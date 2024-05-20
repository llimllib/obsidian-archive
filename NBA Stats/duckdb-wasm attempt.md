---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
- Added esbuild and duckdb-wasm to package.json
- created a dummy file duckdb.js:
```js
import * as duckdb from '@duckdb/duckdb-wasm/dist/duckdb-esm.js';

// the docs (at https://www.npmjs.com/package/@duckdb/duckdb-wasm) list some
// bizarre webpack thing that I don't understand for loading some shit, so
// lets' just choose the jsdelivr option.
//
// I don't like it not being local, but I also want to try and GSD so let's
// settle on this for now
const JSDELIVR_BUNDLES = duckdb.getJsDelivrBundles();

console.log(JSDELIVR_BUNDLES);
```

- Created a make rule:
```makefile
out.js: duckdb.js
	./node_modules/.bin/esbuild duckdb.js --bundle --outfile=out.js
```

- Calling that task doesn't work:
```sh
$ make out.js
./node_modules/.bin/esbuild duckdb.js --bundle --outfile=out.js
 > node_modules/@duckdb/duckdb-wasm/dist/duckdb-esm.js:1:75: error: Could not resolve "apache-arrow" (mark it as external to exclude it from the bundle)
    1 │ ...mWriter as ee,Table as U}from"apache-arrow";import{AsyncByteQueue as Z}f...
      ╵                                 ~~~~~~~~~~~~~~

1 error
make: *** [out.js] Error 1
```

- I see this file for building stuff in the duckdb repo, but idk what the heck it's doing: https://github.com/duckdb/duckdb-wasm/blob/dc65c71e5c19e2aa36a4f4d11ed3ccbc28a04bbf/packages/duckdb-wasm/bundle.mjs
	- it does seem to include a list of dependencies though? maybe I have to install that stuff?
	- `apache-arrow crypto os fs path fast-glob wasm-feature-detect`
		- that list didn't include `stream`, so also install that shit
- hey now `out.js` builds!
	- who knows if it does anything! let's find out
- (side note: now we have a 107mb `node_modules` go go go javascript)
- ok, that compiled, let's try importing and using the silly thing in viewer.js.
	- add this line to the start:
```js
import * as duckdb from '@duckdb/duckdb-wasm/dist/duckdb-esm.js';
```
- then, in the onload, add this hunk which I don't understand _at all_
```js
  const JSDELIVR_BUNDLES = duckdb.getJsDelivrBundles();

  // Select a bundle based on browser checks
  const bundle = await duckdb.selectBundle(JSDELIVR_BUNDLES);

  const worker = new Worker(bundle.mainWorker);
  const logger = new duckdb.ConsoleLogger();
  const db = new duckdb.AsyncDuckDB(logger, worker);
  await db.instantiate(bundle.mainModule, bundle.pthreadWorker);

```

- then change the makefile to build viewer.js instead of the test file
	- it builds but warns about my eval, which hopefully duckdb iwll allow me to pull out anyway
- sadly, loading the file fails in the browser:
```
Uncaught TypeError: class heritage stream_1.Readable is not an object or null

 js http://devd.io:8001/dist/viewer_duckdb.js:13475  

 __require http://devd.io:8001/dist/viewer_duckdb.js:10  

 <anonymous> http://devd.io:8001/dist/viewer_duckdb.js:15606  

 <anonymous> http://devd.io:8001/dist/viewer_duckdb.js:17091  

[viewer_duckdb.js:13475:30](http://devd.io:8001/dist/viewer_duckdb.js)
```

- tried:
	- setting `--platform=esm`, no joy
	- setting `--platform=cjs`, no joy	

ok, I learned more than I ever wanted to about importing stuff with esbuild. We need to alias the `@apache-arrow/esnext-esm` package to `apache-arrow`, because that's the name that duckdb-wasm expects.

Once I vaguely understood the problem, I tried to use [esbuild-plugin-resolve](https://github.com/markwylde/esbuild-plugin-resolve/), but that failed because of [this issue](https://github.com/markwylde/esbuild-plugin-resolve/issues/2) which tries to export default but there's no default to export.

So I took the plugin from that file, removed the line that addres the troublesome import, and created [this build script](https://github.com/llimllib/nbastats/blob/e7f9b2b37314966076b534f5a6235d2b78080dd3/build.mjs), which works.

Now I have a duckdb db that I have no idea how to do anything with!

duckdb sql docs here: https://duckdb.org/docs/sql/introduction

create a table:

```js
const c = await db.connect();
await c.query(`CREATE TABLE weather (
	city VARCHAR,
	temp_lo INTEGER, -- minimum temperature on a day
	temp_hi INTEGER, -- maximum temperature on a day
	prcp REAL,
	date DATE );`);
```

I then tried to show the tables, but it returns a result object I can't figure out how to do anything with:

```js
let res = await c.query("PRAGMA show_tables;")
```

maybe let's try inserting a single row?

```js
 res = await c.query("INSERT INTO weather VALUES ('San Francisco', 46, 50, 0.25, '1994-11-27');")
 ```
 
 OK, to figure out the result API I'm having to read [the tests](https://github.com/duckdb/duckdb-wasm/blob/dc65c71e5c19e2aa36a4f4d11ed3ccbc28a04bbf/packages/duckdb-wasm/test/table_test.ts):
 
 I _think_ the object that gets returned might be apache arrow `table` [object](https://arrow.apache.org/docs/js/)?
 	-	 but it seems to be a little bit different?
	- helpful [observable notebook](https://observablehq.com/@lmeyerov/manipulating-flat-arrays-arrow-style)
	- [this might be the API docs](https://arrow.apache.org/docs/js/classes/Arrow_dom.Table.html) for the table object
	- [this doc](https://observablehq.com/@lmeyerov/manipulating-flat-arrays-arrow-style) suggests there ought to be a `filter` object? but I can't find it
		- I think the doc might be written to an older version of arrow, unfortunately
		- the [table class](https://github.com/apache/arrow/blob/273fab723ce1919c487085e4dbba72eeb669aa5b/js/src/table.ts#L47) doesn't show a filter method
 
 table object:
 - `length`: the number of rows in the table
 - `numCols`: the number of columns
 - `getColumnAt(n)`: return a single column's object
 - `get(n)`: return a row
 ```javascript
// get the first row of the table and print it
>>> table.get(0).toString()  

"{ \"city\": \"San Francisco\", \"temp_lo\": 46, \"temp_hi\": 50, \"prcp\": 0.25, \"date\": Sat Nov 26 1994 19:00:00 GMT-0500 (Eastern Standard Time) }"
```
- `toArray()`: convert the table to an array
	- it's converted into some sort of pointer object rather than copying the data:

```javascript
>>> table.toArray()  
Array [ {} ]
0: Object { Symbol("rowIndex"): 0 }
length: 1
<prototype>: Array []
```
	- but you can convert the array to a string to show all data:

```javascript
>>> table.toArray().join(',')  

"{ \"city\": \"San Francisco\", \"temp_lo\": 46, \"temp_hi\": 50, \"prcp\": 0.25, \"date\": Sat Nov 26 1994 19:00:00 GMT-0500 (Eastern Standard Time) }"
```
- `serialize([encoding], [stream])`: convert the table into a serialized format (parquet maybe?)

```javascript
>>> table.serialize()  

Uint8Array(776) [ 255, 255, 255, 255, 96, 1, 0, 0, 16, 0, … ]

```
- `select([columns])`: pick out a number of columns from the result

```
table.select("city", "temp_lo", "temp_hi").toArray().toString()  

"{ \"city\": \"San Francisco\", \"temp_lo\": 46, \"temp_hi\": 50 }"
```

row object:


column object:
- `get(n)`: return the value of the column at the given row

#### DataFrame

There's a [dataframe](https://arrow.apache.org/docs/js/classes/Arrow_dom.DataFrame.html) object
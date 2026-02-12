---
updated: 2026-02-05T12:09:04.265Z
created: 2024-01-27T21:28:08Z
---
Node has gained the experimental ability to turn a javascript file into a single-file executable by embedding it within a node binary.

However, they have written rather [skimpy instructions](https://nodejs.org/api/single-executable-applications.html) which leave a lot to the imagination. I've written this document to try to give an example that includes multiple files and a dependency.

(update: I found [this document](https://github.com/nodejs/single-executable/blob/main/blog/2022-08-05-an-overview-of-the-current-state.md) which gives a much clearer picture of how the single-file executable process works)

(update feb 5 2026: Joyee Cheung [improved the process greatly](https://joyeecheung.github.io/blog/2026/01/26/improving-single-executable-application-building-for-node-js/). Great work, and thank you!)

I've created a GitHub repository [llimllib/node-esbuild-executable](https://github.com/llimllib/node-esbuild-executable) to demonstrate the topics discussed here.

(All this is on a mac. Instructions vary for your platform, but will be similar)

- `npm init -y` to create a new package
- let's install a package: `npm add --save minimist`
- enable ESM modules by adding `"type": "module"` to `package.json`
- Create a simple two-file program that uses our dependency, so we can simulate something vaguely realistic:

**sum.js**
```javascript
export function sum(ns) { return ns.reduce((x,y) => x+y, 0) }
```

**index.js**
```javascript
import minimist from "minimist";
import { sum } from "./sum.js";

sum(minimist(process.argv.slice(2))._)
```

We can test that this simple program works to sum the numbers input into it:

```console
$ node index.js 1 2 3 4
10
```

- Create an SEA config file. This tells node what file to use for input and how to output your executable; the options are [documented here](https://nodejs.org/api/single-executable-applications.html#generating-single-executable-applications-with---build-sea) but we only need two
**sea-config.json**
```javascript
{ 
  "main": "index.js", 
  "output": "sum"  
}
```
- run `node --build-sea sea-config.json`
- Sign the new binary: `codesign --sign - sum`
- Run the script, and note that it fails!

```
$ ./sum 1 2 3 4 5      
(node:39271) Warning: To load an ES module, set "type": "module" in the package.json or use the .mjs extension.
(Use `sea-example --trace-warnings ...` to show where the warning was created)
/private/tmp/test-sea/sea-example:1
import minimist from "minimist";
^^^^^^

SyntaxError: Cannot use import statement outside a module
    at internalCompileFunction (node:internal/vm:73:18)
    at wrapSafe (node:internal/modules/cjs/loader:1175:20)
    at embedderRunCjs (node:internal/util/embedding:18:27)
    at node:internal/main/embedding:18:34

Node.js v20.2.0
```

## bundling it all up

There's (at least) two problems with the binary we built:
- it doesn't include the `minimist` library which is a dependency of our script
- our code inside the binary is attempting to load an ES module, which is unsupported in a SEA program.

The docs say:

> The single executable application feature currently only supports running a single embedded script using the [CommonJS](https://nodejs.org/api/modules.html#modules-commonjs-modules) module system.

We can fix both of these problems by using [esbuild](https://esbuild.github.io/) to bundle up our code with its dependencies, and convert it into a single cjs module that will work correctly in our binary.

-  install esbuild: `npm add --save-dev esbuild`
-  run esbuild to create a bundle, and save it to `bundle.js`:
	```
	npx esbuild \
		--format=cjs \
		--target=node20 \
		--platform=node \
		--bundle \
		--outfile=bundle.js \ 
		index.js
	```
- change `index.js` to `bundle.js` in your sea config file
- re-build the binary: `node --build-sea sea-config.json`
- and sign it: `codesign --sign - sum`

This time, it works!

```console
$ ./sum 1 2 3 4        
10
(node:44573) ExperimentalWarning: Single executable application is an experimental feature and might change at any time
(Use `sum --trace-warnings ...` to show where the warning was created)

# `sum` is an executable binary:
$ file sum
sum: Mach-O 64-bit executable arm64

# that weighs 82 megabytes:
$ ls -alh sum
-rwxr-xr-x@ 1 llimllib  staff    82M Jan 27 16:11 sum*
```

One thing you'll notice is that it prints a warning after executing the program. To remove the warning, add `"disableExperimentalSEAWarning": true` to your `sea-config.json`.
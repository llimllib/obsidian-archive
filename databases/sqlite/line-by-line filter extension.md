---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/asg017/sqlite-lines

> `sqlite-lines` is a SQLite extension for reading lines from a file or blob.

> `sqlite-lines` is great for line-oriented datasets, like [ndjson](https://ndjson.org/) or [JSON Lines](https://jsonlines.org/), when paired with SQLite's [JSON support](https://www.sqlite.org/json1.html). Here, we calculate the top 5 country participants in Google's [Quick, Draw!](https://quickdraw.withgoogle.com/data) dataset for [`calendars.ndjson`](https://storage.googleapis.com/quickdraw_dataset/full/simplified/calendar.ndjson):

```sql
select
  line ->> '$.countrycode' as countrycode,
  count(*)
from lines_read('./calendar.ndjson')
group by 1
order by 2 desc
limit 5;
/*
┌─────────────┬──────────┐
│ countrycode │ count(*) │
├─────────────┼──────────┤
│ US          │ 141001   │
│ GB          │ 22560    │
│ CA          │ 11759    │
│ RU          │ 9250     │
│ DE          │ 8748     │
└─────────────┴──────────┘
*/
```

Really nice observable notebook [here](https://observablehq.com/@asg017/introducing-sqlite-lines) with:

- example of usage
- how to build a sqlite extension
- how to compile to wasm sqlite with an extension
- how to compile a custom sqlite binary with an extension
- demo of a [simple CLI tool](https://github.com/asg017/sqlite-lines#the-sqlite-lines-cli) built with this:

```
$ cat names.txt | sqlite-lines 'rowid || upper(d)'
1ALEX
2BRIAN
3CRAIG
```
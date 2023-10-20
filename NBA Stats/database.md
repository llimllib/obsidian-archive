I made a build using SQLite, but it was too painful to use - the lack of quantile queries for example was painful. I solved it with a horrible query, but it was just too much.

It's very unfortunate that [sql.js](https://github.com/sql-js/sql.js/), a very useful and neat project, [does not support custom aggregation functions](https://github.com/sql-js/sql.js/issues/204)

It might be possible to use [[Duckdb]] instead, with its WASM engine?
- hey today 10/29 they wrote a blog post about duckdb-wasm! https://duckdb.org/2021/10/29/duckdb-wasm.html
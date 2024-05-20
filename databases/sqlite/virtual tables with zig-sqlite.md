---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
[https://rischmann.fr/blog/virtual-tables-with-zig-sqlite](https://rischmann.fr/blog/virtual-tables-with-zig-sqlite)

> [Virtual tables](https://sqlite.org/vtab.html) let you expose almost anything as a SQL table: this is powerful because you can then use all the power of SQLite and SQL to exploit it. Ever wanted to join a CSV, a JSON file and a REST API? Virtual tables let you do that.

> My goals for this feature were:

> -   providing a nice Zig API to implement a virtual table
> -   allow building a virtual table as a [loadable extension](https://sqlite.org/loadext.html)

> Today I want to talk about how I implemented it and I’ll also talk about a small demo I made.

The demo is a virtual table that actually hits an API instead of storing the data

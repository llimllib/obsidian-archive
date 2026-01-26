---
created: 2026-01-26T02:35:54.778Z
updated: 2026-01-26T02:35:54.778Z
---
https://dlt.github.io/blog/posts/introduction-to-postgresql-indexes/

> This text is for developers that have an intuitive knowledge of what database indexes are, but don’t necessarily know how they work internaly, what are the tradeoffs associated with indexes, what are the types of indexes provided by postgres and how you can use some of its more advanced options to make them more optimized for your use case.

I haven't worked with postgres in a long time and I'm excited to get to work with it again at my new job!

new to me is `show data_directory;`, which prints the storage directory for the postgres instance you're on. Also, I did not know that data was stored in the `<data dir>/<oid of database>/<oid of table>` file - I'd seen those numbers before and not known what they referred to.

I had forgotten too that indexes can be partial: `create index on rules(status) where status = 'enabled';`, very useful for tables with soft-deletion

Also the [news.yc comments](https://news.ycombinator.com/item?id=46751826) indicate that the articles' note about multi-column indexes (that postgres can only use them in order) is no longer accurate, as [postgres 18 added skip scans](https://neon.com/postgresql/postgresql-18/skip-scan-btree)
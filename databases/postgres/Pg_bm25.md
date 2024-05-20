---
updated: '2024-02-12T16:32:58Z'
created: '2024-02-12T16:32:58Z'
---
https://blog.paradedb.com/pages/introducing_bm25
https://github.com/paradedb/paradedb/

> `pg_bm25` aims to bridge the gap between the native capabilities of Postgres’ full text search and those of a specialized search engine like Elasticsearch. The goal is to eliminate the need to bring a cumbersome service like Elasticsearch into the data stack.

—-

> In 2016, an open source search library called [Tantivy](https://github.com/quickwit-oss/tantivy) emerged. Tantivy was designed as a Rust-based alternative to Apache Lucene, the search library that powers Elasticsearch. Three years later, a library called [pgrx](https://github.com/pgcentralfoundation/pgrx) — built by the same author of ZomboDB — made it possible to build Postgres extensions in Rust. Combined, these projects laid the groundwork for a Postgres extension that could create Elastic-quality search experiences within Postgres.

———

> On a table with one million rows, `pg_bm25`indexes 50 seconds faster than `tsvector`and ranks results 20x faster. Indexing and search times are nearly identical to those of a dedicated Elasticsearch instance.
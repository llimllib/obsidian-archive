---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://docs.paradedb.com/blog/introducing_bm25
https://github.com/paradedb/paradedb/tree/800ff3e6/pg_bm25

> We’re unveiling pg_bm25: a Rust-based Postgres extension that significantly improves Postgres’ full text search capabilities. pg_bm25 is named after BM25, the algorithm used by modern search engines to calculate the relevance scores of search results.

> - 100% Postgres native, with zero dependencies on an external search engine
> - Built on top of Tantivy, a Rust-based alternative to the Apache Lucene search library
> - Support for fuzzy search, aggregations, highlighting, and relevance tuning
> - Real-time search — new data is immediately searchable without manual reindexing
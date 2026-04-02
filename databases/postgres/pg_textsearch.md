---
created: 2026-04-01T20:50:05.931Z
updated: 2026-04-01T20:50:05.931Z
---
https://github.com/timescale/pg_textsearch
https://www.tigerdata.com/docs/use-timescale/latest/extensions/pg-textsearch

explanatory blog post: https://www.tigerdata.com/blog/pg-textsearch-bm25-full-text-search-postgres

> If you have used Postgres's built-in ts_rank for full-text search at any meaningful scale, you already know the limitations. Ranking quality degrades as your corpus grows. There is no inverse document frequency, so common words carry the same weight as rare ones. There is no term frequency saturation, so a document that mentions "database" 50 times outranks one that mentions it once. There is no efficient top-k path: scoring requires touching every matching row.

> Most teams work around this by bolting on Elasticsearch or Typesense as a sidecar. That works, but now you are syncing data between two systems, operating two clusters, and debugging consistency issues when they diverge.

> [pg_textsearch](https://www.tigerdata.com/docs/use-timescale/latest/extensions/pg-textsearch) takes a different approach: real BM25 scoring, built from scratch in C on top of Postgres's own storage layer. You create an index, write a query, and get results ranked by relevance:
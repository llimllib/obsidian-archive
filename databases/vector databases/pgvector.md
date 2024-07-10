---
created: 2024-07-10T13:56:24.818Z
updated: 2024-07-10T13:56:24.818Z
---
https://github.com/pgvector/pgvector
https://docs.timescale.com/use-timescale/latest/extensions/pgvector/?ref=timescale.com

> The `pgvector` PostgreSQL extension helps you to store and search over machine learning-generated embeddings. It provides different capabilities that allows you to identify both exact and approximate nearest neighbors. It is designed to work seamlessly with other PostgreSQL features, including indexing and querying.

Appears to contain its own hnsw implementation, which is neat.

Also has bindings to a bunch of libraries, even though anything with a postgres driver will work with it.

Timescale has a [tutorial](https://www.timescale.com/blog/postgresql-as-a-vector-database-create-store-and-query-openai-embeddings-with-pgvector/) on its use.
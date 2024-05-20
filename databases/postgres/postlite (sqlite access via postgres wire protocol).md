---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/benbjohnson/postlite

> Postlite is a network proxy to allow access to remote SQLite databases over the Postgres wire protocol. This allows GUI tools to be used on remote SQLite databases which can make administration easier.

> The proxy works by translating Postgres frontend wire messages into SQLite transactions and converting results back into Postgres response wire messages. Many Postgres clients also inspect the `pg_catalog` to determine system information so Postlite mirrors this catalog by using an attached in-memory database with virtual tables. The proxy also performs minor rewriting on these system queries to convert them to usable SQLite syntax.
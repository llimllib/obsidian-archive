---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
## Jet

https://github.com/go-jet/jet

> Jet is a complete solution for efficient and high performance database access, consisting of type-safe SQL builder with code generation and automatic query result data mapping.  
Jet currently supports `PostgreSQL`, `MySQL`, `MariaDB` and `SQLite`. Future releases will add support for additional databases.

## ent

[[ent]]
https://entgo.io/
https://github.com/ent/ent

Simple, yet powerful entity framework for Go, that makes it easy to build and maintain applications with large data-models.

-   **Schema As Code** - model any database schema as Go objects.
-   **Easily Traverse Any Graph** - run queries, aggregations and traverse any graph structure easily.
-   **Statically Typed And Explicit API** - 100% statically typed and explicit API using code generation.
-   **Multi Storage Driver** - supports MySQL, MariaDB, TiDB, PostgreSQL, SQLite and Gremlin.
-   **Extendable** - simple to extend and customize using Go templates.

## sqlc

https://sqlc.dev/
https://github.com/kyleconroy/sqlc

sqlc generates **type-safe code** from SQL. Here's how it works:

1.  You write queries in SQL.
2.  You run sqlc to generate code with type-safe interfaces to those queries.
3.  You write application code that calls the generated code.

## sqlboiler

https://github.com/volatiletech/sqlboiler

SQLBoiler is a tool to generate a Go ORM tailored to your database schema.

It is a "database-first" ORM as opposed to "code-first" (like gorm/gorp). That means you must first create your database schema. Please use something like [sql-migrate](https://github.com/rubenv/sql-migrate) or some other migration tool to manage this part of the database's life-cycle.

## xo
https://github.com/xo/xo

> `xo` is a command-line tool to generate _idiomatic_ code for different languages code based on a database schema or a custom query.

its author was very rude to me when I asked a question on the gopher slack, so I prefer not to use this library any longer 🤷‍♂️

## gorm

I'm not a fan of runtime ORM for go (or in general...), but I'll include it here for completeness

https://gorm.io/index.html

> The fantastic ORM library for Golang, aims to be developer friendly.

## squirrel

Not an entity framework or database mapper, but tool for building sql queries at runtime

Squirrel helps you build SQL queries from composable parts:

```
import sq "github.com/Masterminds/squirrel"

users := sq.Select("*").From("users").Join("emails USING (email_id)")

active := users.Where(sq.Eq{"deleted_at": nil})

sql, args, err := active.ToSql()

sql == "SELECT * FROM users JOIN emails USING (email_id) WHERE deleted_at IS NULL"
```
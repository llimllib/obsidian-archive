https://github.com/supabase/postgres_lsp

> A Language Server for Postgres. Not SQL with flavors, just Postgres.

neat!

> Despite the rising popularity of Postgres, support for the PL/pgSQL in IDEs and editors is limited. While there are some _generic_ SQL Language Servers[1](https://github.com/supabase/postgres_lsp#user-content-fn-1-5e666cb9001b13365e41a573df7bb596) offering the Postgres syntax as a "flavor" within the parser, they usually fall short due to the ever-evolving and complex syntax of PostgreSQL. There are a few proprietary IDEs[2](https://github.com/supabase/postgres_lsp#user-content-fn-2-5e666cb9001b13365e41a573df7bb596) that work well, but the features are only available within the respective IDE.

> This Language Server is designed to support Postgres, and only Postgres. The server uses [libpg_query](https://github.com/pganalyze/libpg_query), therefore leveraging the PostgreSQL source to parse the SQL code reliably. Using Postgres within a Language Server might seem unconventional, but it's the only reliable way of parsing all valid PostgreSQL queries. You can find a longer rationale on why This is the Way™ [here](https://pganalyze.com/blog/parse-postgresql-queries-in-ruby). While libpg_query was built to execute SQL, and not to build a language server, any shortcomings have been successfully mitigated in the `parser` crate. You can read the [commented source code](https://github.com/supabase/postgres_lsp/blob/main/crates/parser/src/lib.rs) for more details on the inner workings of the parser.
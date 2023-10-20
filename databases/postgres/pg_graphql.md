A competitor to [[Postgraphile]] has arisen: `pg_graphql` from the [[supabase]] folks

https://github.com/supabase/pg_graphql

[Introduction post](https://supabase.com/blog/2021/12/03/pg-graphql):

> Today we're open sourcing [`pg_graphql`](https://github.com/supabase/pg_graphql), a work-in-progress native PostgreSQL extension adding GraphQL support. The extension keeps schema generation, query parsing, and resolvers all neatly contained on your database server requiring no external services.

> We found both options [postgraphile and hasura] to be largely viable for the core feature set.

> Which left us with one final hang-up: we host free-tier projects on VMs with 1 GB of memory. After tallying the resources reserved for PostgreSQL, PostgREST, Kong, GoTrue, and a handful of smaller services, we were left with a total memory budget of ... 0 MB 😬. Unsurprisingly, our pathological memory target disqualified any option that required launching another process in those VMs.

> For that reason, we decided to invest in a lightweight alternative that runs in the database, and can be exposed over HTTP using the existing [PostgREST](https://supabase.com/docs/guides/api) deployments' [RPC functionality.](https://postgrest.org/en/v8.0/api.html#stored-procedures)

[[Postgres]] and [[GraphQL]]

pg_graphql is [now available on supabase](https://supabase.com/blog/2022/03/29/graphql-now-available)
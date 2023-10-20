REST server for [[Postgres]], using row-level security you can directly query your database. Used extensively by supabase.

https://postgrest.org/

> ## Motivation[](https://postgrest.org/en/v9.0/#motivation "Permalink to this headline")

> Using PostgREST is an alternative to manual CRUD programming. Custom API servers suffer problems. Writing business logic often duplicates, ignores or hobbles database structure. Object-relational mapping is a leaky abstraction leading to slow imperative code. The PostgREST philosophy establishes a single declarative source of truth: the data itself.

> ## Declarative Programming[](https://postgrest.org/en/v9.0/#declarative-programming "Permalink to this headline")

> It’s easier to ask PostgreSQL to join data for you and let its query planner figure out the details than to loop through rows yourself. It’s easier to assign permissions to db objects than to add guards in controllers. (This is especially true for cascading permissions in data dependencies.) It’s easier to set constraints than to litter code with sanity checks.

I like the idea, but I also worry about sticking the database server with the job of serving HTTP requests?

I like having an app layer as a policy & scaling layer, but maybe I'm just being precious. computers are fast these days.
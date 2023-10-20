# migra

https://github.com/djrobstep/migra

> `migra` is a schema diff tool for [[Postgres]], written in Python. Use it in your python scripts, or from the command line like this:

```
$ migra postgresql:///a postgresql:///b
alter table "public"."products" add column newcolumn text;

alter table "public"."products" add constraint "x" CHECK ((price > (0)::numeric));
```

> `migra` magically figures out all the statements required to get from A to B.

> Most features of PostgreSQL are supported.

> Schema migrations are without doubt the most cumbersome and annoying part of working with SQL databases. So much so that some people think that schemas themselves are bad!

> But schemas are actually good. Enforcing data consistency and structure is a good thing. It’s the migration tooling that is bad, because it’s harder to use than it should be. `migra` is an attempt to change that, and make migrations easy, safe, and reliable instead of something to dread.

# Goose

https://github.com/pressly/goose

> Goose is a database migration tool. Manage your database schema by creating incremental SQL changes or Go functions.

# atlas

https://atlasgo.io/

[[ent]]'s underlying migration tool

> Atlas DDL is a declarative, Terraform-like configuration language designed to capture an organization’s data topology. Currently, it supports defining schemas for SQL databases such as MySQL, Postgres, SQLite and MariaDB.

how it handles migration conflicts: https://entgo.io/blog/2022/05/09/versioned-migrations-sum-file/

> The `atlas.sum` file contains a sum of the whole directory as its first entry, and a checksum for each of the migration files (implemented by a reverse, one branch merkle hash tree)... As you can see the `atlas.sum` file contains one entry for each migration file generated. With the `atlas.sum` generation file enabled, both Team A and Team B will have such a file once they generate migrations for a schema change. Now the version control will raise a merge conflict once the second Team attempts to merge their feature.

---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://gist.github.com/jcoleman/1e6ad1bf8de454c166da94b67537758b

This is basically what we tried to do on MCT, but thought through more thoroughly. Some info outdated, but still very useful.

(Tried to find the original source but wasn't able to)

HN comment:

>  Something that doesn't appear to be mentioned in here that bit me recently is that views follow a table through renames. Ended up having views that were subtly broken because they were pointing to the tables that I had renamed to have an `_old` suffix instead of the newly created ones I had expected them to point to.

With a response listing a good idea for how to make this more visible:

> This is a very good example of why you should be using a schema diff/comparison tool.

> Run your rename on a copy of your production schema, then run a diff tool to see what's actually changed - in this case it would show a view definition had changed and even autogenerate the replace statement you would need to add to fix the script.

Another comment points out a change in the meantime:

>  Worth noting that with Postgres 12+ you can REINDEX CONCURRENTLY so no need for the 3-step process mentioned in this gist.

Another commenter gives a link to a project he's working on https://github.com/fabianlindfors/reshape:

> Reshape is an easy-to-use, zero-downtime schema migration tool for Postgres. It automatically handles complex migrations that would normally require downtime or manual multi-step changes. During a migration, Reshape ensures both the old and new schema are available at the same time, allowing you to gradually roll out your application. It will also perform all changes without excessive locking, avoiding downtime caused by blocking other queries. For a more thorough introduction to Reshape, check out the [introductory blog post](https://fabianlindfors.se/blog/schema-migrations-in-postgres-using-reshape/).

> Designed for Postgres 12 and later.
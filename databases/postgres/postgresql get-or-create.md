---
created: 2024-08-05T13:27:11.079Z
updated: 2024-08-05T13:27:11.079Z
---
https://hakibenita.com/postgresql-get-or-create

A thorough document about how to implement the "get or create" pattern in postgres, which demonstrates excellent facility with the database throughout.

It's surprisingly difficult to get right!

I learned about:

- `ON CONFLICT DO NOTHING`
- the `RETURNING` statement in a CTE
- the difference between `UNION` and `UNION ALL` (the latter doesn't check for duplicate rows, so if you know there can't be duplicates in your query, it's more efficient)
- `MERGE`
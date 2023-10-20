https://antonz.org/sqlean-define/

a short post about the `define` function from sqlean:

> SQLite provides an extension mechanism. One of such extensions — `define` — allows writing functions in regular SQL.

> With `define` writing a custom function becomes as easy as:

```sql
select define('sumn', ':n * (:n + 1) / 2');
```

> And then using it as any built-in function:

```sql
> select sumn(5);
15
```
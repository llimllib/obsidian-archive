https://ibis-project.org/docs/3.0.2/tutorial/01-Introduction-to-Ibis/

> Ibis is a Python framework to access data and perform analytical computations from different sources, in a standard way.

> In a way, you can think of Ibis as writing SQL in Python, with a focus on analytics, more than simply accessing data. And aside from SQL databases, you can use it with other backends, including big data systems.

> Why not simply use SQL instead? SQL is great and widely used. However, SQL has different flavors for different database engines, and SQL is very difficult to maintain when your queries are very complex. Ibis solves both problems by standardizing your code across backends and making it maintainable. Since Ibis is Python, you can structure your code in different files, functions, name variables, write tests, etc.

Can run against [[sqlite]], [[Postgres]], or [[bigquery]].

ex:

```python
t.group_by("f").aggregate(d=t.a + t.b.sum())
```

gets transformed to something like (depending on the db):

```sql
SELECT f, sum(a + b) AS d
FROM t
GROUP BY f
```

Found via [this issue](https://github.com/duckdb/duckdb/issues/2000#issuecomment-880885788) describing [[Duckdb]]'s roadmap for gaining a pandas-like interface (in the python version anyway).

I kind of want to develop a similar thing for javascript.
https://ibis-project.org/tutorials/getting_started

> Ibis is the portable Python dataframe library.

> If you’ve had issues with scaling data transformation code in Python, need to work with data in multiple data platforms, find yourself translating between other Python dataframe APIs, or just want a great Python dataframe experience, Ibis is for you.

Runs against [[Duckdb]] by default, but can run against [[polars]], [[sqlite]], [[Postgres]], and lots of others.

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
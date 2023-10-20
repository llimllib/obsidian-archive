https://rednafi.github.io/reflections/recipes-from-python-sqlite-docs.html

> While going through the documentation of Python's [`sqlite3`](https://docs.python.org/3/library/sqlite3.html) module, I noticed that it's quite API-driven, where different parts of the module are explained in a prescriptive manner. I, however, learn better from examples, recipes, and narratives. Although a few good recipes already exist in the docs, I thought I'd also enlist some of the examples I tried out while grokking them.

example of user-defined functions:

```python
# src.py
import sqlite3
import hashlib

conn = sqlite3.connect(":memory:")
c = conn.cursor()


def sha256(t: str) -> str:
    return hashlib.sha256(
        t.encode("utf-8"),
        usedforsecurity=True,
    ).hexdigest()


# Register the scalar function.
conn.create_function("sha256", 1, sha256)

with conn:
    c.execute(
        """
        create table if not exists users (
            username text,
            password text
        );
    """
    )
    c.execute(
        "insert into users values (?, sha256(?));",
        ("admin", "password"),
    )
    c.execute(
        "insert into users values (?, sha256(?));",
        ("user", "otherpass"),
    )

    result = c.execute("select * from users;").fetchall()
    print(result)
```
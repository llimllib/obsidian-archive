https://antonz.org/sqlean/

I really like [[sqlite]]. It’s a miniature embedded database, perfect for both exploratory data analysis and as a storage for small apps (I’ve [blogged about that](https://antonz.org/sqlite-is-not-a-toy-database/) previously).

It has a minor drawback though. There are few built-in functions compared to PostgreSQL or Oracle. Fortunately, the authors provided an extension mechanism, which allows doing almost anything. As a result, there are a lot of SQLite extensions out there, but they are incomplete, inconsistent and scattered across the internet.

I wanted more consistency. So I started the **sqlean** project, which brings the extensions together, neatly packaged into domain modules, documented, tested, and built for Linux, Windows and macOS. Something like a standard library in Python or Go, only for SQLite.

----

https://github.com/nalgeon/sqlean.py

A python project that provides a dropin sqlite package replacement with sqlean available
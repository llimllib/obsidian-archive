---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://www.sqlite.org/vtab.html

> A virtual table is an object that is registered with an open SQLite [database connection](https://www.sqlite.org/c3ref/sqlite3.html). From the perspective of an SQL statement, the virtual table object looks like any other table or view. But behind the scenes, queries and updates on a virtual table invoke callback methods of the virtual table object instead of reading and writing on the database file.

> The virtual table mechanism allows an application to publish interfaces that are accessible from SQL statements as if they were tables. SQL statements can do almost anything to a virtual table that they can do to a real table, with the following exceptions:

List of the virtual tables that come with SQLite: https://www.sqlite.org/vtablist.html

includes JSON, CSV, rtree, and lots of metadata about the sqlite database itself.

Protobuf virtual table: https://github.com/rgov/sqlite_protobuf

Histogram virtual tables: https://github.com/Oeffner/SQLiteHistograms


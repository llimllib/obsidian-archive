---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://sqlite.org/hctree/doc/hctree/doc/hctree/index.html

> SQLite is sometimes used as the core of a client/server database system. While it works reliably well in such cases, the database backend module that it uses to store b-tree structures in its database file was not designed with this case in mind and can be improved upon in several ways. The HC-tree (hctree) project is an attempt to develop a new database backend that improves upon regular SQLite as follows:
> - **Improved concurrency:** Stock SQLite is limited to a single concurrent writer. Hctree uses optimistic row-level locking and is designed to support dozens of concurrent writers running at full-speed.
> - **Support for replication:** Stock SQLite supports the [sessions extension](http://sqlite.org/sessionintro.html), which allows the contents of a committed transaction to be serialized for tranmission and application to a second database... Hctree builds this into the database backend
> - **Removal of database size limitations:**   Hctree uses 48-bit page numbers, allowing 2^60 byte databases, or 1EiB. Roughly one million TiB.
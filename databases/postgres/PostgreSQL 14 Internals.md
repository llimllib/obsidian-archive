https://postgrespro.com/community/books/internals

> This book is for those who will not settle for a black-box approach when working with a database. Briefly touching upon the main concepts of PostgreSQL, the book then plunges into the depths of data consistency and isolation, explaining implementation details of multiversion concurrency control and snapshot isolation, buffer cache and write-ahead log, and the locking system. The rest of the book covers the questions of planning and executing SQL queries, including the discussion of data access and join methods, statistics, and various index types.

The first two parts are done and available freely:

-   Part I. Isolation and MVCC
    
    Isolation · Pages and Tuples · Snapshots · Page Pruning and HOT Updates · Vacuum and Autovacuum · Freezing · Rebuilding Tables and Indexes
    
-   Part II. Buffer Cache and WAL
    
    Buffer Cache · Write-Ahead Log · WAL Modes
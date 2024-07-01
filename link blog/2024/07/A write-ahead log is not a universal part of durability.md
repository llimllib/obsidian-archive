---
created: 2024-07-01T13:16:11.044Z
updated: 2024-07-01T13:16:11.044Z
---
https://notes.eatonphil.com/2024-07-01-a-write-ahead-log-is-not-a-universal-part-of-durability.html

A nice tour through what durability is, why you might want a write-ahead log, and what they do and do not bring to the table.

If you want a dive into a particular WAL, I was reminded of [this post from Ben Johnson](https://fly.io/blog/sqlite-internals-wal/) about the [[sqlite]] WAL, which I'm surprised I haven't previously linked in these notes.

That post is part of a series about how SQLite works from the excellent Ben Johnson:

- [SQLite internals: pages & b-trees](https://fly.io/blog/sqlite-internals-btree/)
- [How SQLite helps you do ACID](https://fly.io/blog/sqlite-internals-rollback-journal/)
- [How the SQLite virtual machine works](https://fly.io/blog/sqlite-virtual-machine/)
- [How SQLite scales read concurrency](https://fly.io/blog/sqlite-internals-wal/)
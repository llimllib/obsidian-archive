---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
- [[sqlite3vfshttp]]
- https://github.com/psanford/donutdb
	- dynamodb as a backing store for sqlite via VFS. Very neat!
- https://github.com/litements/s3sqlite
	- This VFS enables reading databases from S3 using [s3fs](https://s3fs.readthedocs.io/en/latest/index.html). This only supports reading operations, any operation that tries to modify the DB file is ignored.
	- Inspired by [sqlite-s3vfs](https://github.com/uktrade/sqlite-s3vfs) and [sqlite-s3-query](https://github.com/michalc/sqlite-s3-query).
- https://pkg.go.dev/go.gazette.dev/core@v0.89.0/consumer/store-sqlite
	- The central strategy of this package is to provide a SQLite VFS implementation ([https://www.sqlite.org/vfs.html](https://www.sqlite.org/vfs.html)) with "hooks" to record mutations of these files made by the database, as they occur, into a recovery log. Recovering a database consists of restoring the on-disk representation of the main database and associated transaction logs.
	- I can't say I understand this one exactly - it mentions that it implements the `consumer.Store` interface, but... not what that is
		- The commenter on the [news.yc](https://news.ycombinator.com/item?id=32828799) article says:
		- > Here's a particularly crazy one which offers synchronous, low-latency (millis) replication of a SQLite database to a distributed recovery log. It does this by instrumenting the file operations SQLite is making and recording their effects into the log.
- [this article](https://phiresky.github.io/blog/2021/hosting-sqlite-databases-on-github-pages/) describes the technique in general
- Not exactly the same, but a commenter links the [s3 select](https://docs.aws.amazon.com/AmazonS3/latest/userguide/selecting-content-from-objects.html) functionality, which is neat:
	- > With Amazon S3 Select, you can use simple structured query language (SQL) statements to filter the contents of an Amazon S3 object and retrieve just the subset of data that you need. By using Amazon S3 Select to filter this data, you can reduce the amount of data that Amazon S3 transfers, which reduces the cost and latency to retrieve this data.
	- works on CSV, Json or Parquet files
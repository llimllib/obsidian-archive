https://github.com/psanford/sqlite3vfshttp

> sqlite3vfshttp is a sqlite3 VFS for querying remote databases over http(s). This allows you to perform queries without needing to download the complete database first.

> Your database must be hosted on a webserver that supports HTTP range requests (such as Amazon S3).

in golang. Related to [[Statically hosted sqlite with range queries]]

> See [sqlitehttpcli/sqlitehttpcli.go](https://github.com/psanford/sqlite3vfshttp/blob/main/sqlitehttpcli/sqlitehttpcli.go) for a simple CLI tool that is able to query a remotely hosted sqlite database.

neat that you can do it locally!
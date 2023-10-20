https://github.com/phiresky/sql.js-httpvfs

> See my blog post for an introduction: [https://phiresky.github.io/blog/2021/hosting-sqlite-databases-on-github-pages/](https://phiresky.github.io/blog/2021/hosting-sqlite-databases-on-github-pages/)

> sql.js is a light wrapper around SQLite compiled with EMScripten for use in the browser (client-side).

> This repo is a fork of and wrapper around sql.js to provide a read-only HTTP-Range-request based virtual file system for SQLite. It allows hosting an SQLite database on a static file hoster and querying that database from the browser without fully downloading it.

Read-only of course, but very interesting! Would be fun to figure out what an absolutely minimal policy layer for a [[sqlite]] database would look like to enable writes
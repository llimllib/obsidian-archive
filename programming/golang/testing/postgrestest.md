---
created: 2024-11-19T18:47:26.739Z
updated: 2024-11-19T18:47:26.739Z
---
https://pkg.go.dev/zombiezen.com/go/postgrestest

> Package `postgrestest` provides a test harness that starts an ephemeral [PostgreSQL](https://www.postgresql.org/) server. It is tested on macOS, Linux, and Windows. It can cut down the overhead of PostgreSQL in tests up to 90% compared to spinning up a `postgres` Docker container: starting a server with this package takes roughly 650 milliseconds and creating a database takes roughly 20 milliseconds.

via [this article](https://michael.stapelberg.ch/posts/2024-11-19-testing-with-go-and-postgresql-ephemeral-dbs/), where the author actually uses [their own fork](https://pkg.go.dev/github.com/stapelberg/postgrestest); it's unclear to me how they differ.

The article does a good job explaining how to spin this up at the beginning of a go test run.
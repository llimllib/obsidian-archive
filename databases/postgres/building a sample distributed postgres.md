https://notes.eatonphil.com/distributed-postgres.html

uses [[golang]] libraries to demonstrate how you could build a very simplified version of a distributed postgres

> What is [[CockroachDB]] under the hood? Take a look at [its go.mod](https://github.com/cockroachdb/cockroach/blob/master/go.mod) and notice a number of dependencies that do a lot of work: [a PostgreSQL wire protocol implementation](https://github.com/jackc/pgproto3), [a storage layer](https://github.com/cockroachdb/pebble), [a Raft implementation for distributed consensus](https://github.com/etcd-io/etcd). And not part of go.mod but still building on 3rd party code, [PostgreSQL's grammar definition](https://github.com/cockroachdb/cockroach/blob/master/pkg/sql/parser/sql.y).

> To be _absurdly_ reductionist, CockroachDB is just the glue around these libraries. With that reductionist mindset, let's try building a distributed Postgres proof of concept ourselves!
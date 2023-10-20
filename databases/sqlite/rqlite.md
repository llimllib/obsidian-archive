[rqlite](https://github.com/rqlite/rqlite) 

> _rqlite_ is an easy-to-use, lightweight, distributed relational database, which uses [SQLite](https://www.sqlite.org/) as its storage engine. rqlite is simple to deploy, operating it is very straightforward, and its clustering capabilities provide you with fault-tolerance and high-availability. [rqlite is available for Linux, macOS, and Microsoft Windows](https://github.com/rqlite/rqlite/releases).

### Why?

> rqlite gives you the functionality of a [rock solid](https://www.sqlite.org/testing.html), fault-tolerant, replicated relational database, but with very **easy installation, deployment, and operation**. With it you've got a **lightweight** and **reliable distributed relational data store**. Think [etcd](https://github.com/coreos/etcd/) or [Consul](https://github.com/hashicorp/consul), but with relational data modelling also available.
>
> You could use rqlite as part of a larger system, as a central store for some critical relational data, without having to run larger, more complex distributed databases.
> 
> Finally, if you're interested in understanding how distributed systems actually work, **rqlite is a good example to study**. Much thought has gone into its [design](https://github.com/rqlite/rqlite/blob/master/DOC/DESIGN.md) and implementation, with clear separation between the various components, including storage, distributed consensus, and API.

Uses [[sqlite]] as a source database
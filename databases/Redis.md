https://redis.io/

in-memory data structure server

Redis recently (March 2024) removed the BSD license and is no longer open source software.

Some open source forks of it include:

- [KeyDB](https://docs.keydb.dev/)
	- performance-focused multithreaded redis
- [redict](https://codeberg.org/redict/redict)
	- by Drew DeVault et al, this branch will attempt to stay closer to redis, rename everything to `redict`
	- [blog post announcement](https://redict.io/posts/2024-03-22-redict-is-an-independent-fork/)
- [valkey](https://github.com/valkey-io/valkey)
	- The Linux Foundation's fork
	- via [this LWN piece](https://lwn.net/SubscriberLink/966631/6bf2063136effa1e/)
- [kvrocks](https://github.com/apache/kvrocks)
	- an Apache Foundation alternative
	- > Apache Kvrocks is a distributed key value NoSQL database that uses RocksDB as storage engine and is compatible with Redis protocol. 
- [garnet](https://github.com/microsoft/garnet)
	- A C# redis-protocol server from microsoft
	- The idea of running a dotnet server is completely anathema to me, I have no interest in this one
---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/dragonflydb/dragonfly

Attempting to be a much faster alternative to [[redis]]. Currently in pre-alpha.

Lots of discussion on [news.yc](https://news.ycombinator.com/item?id=31560547) about why and if it's currently so fast. Some ideas:

- use of multiple threads and fibers
- use of [io_uring](https://kernel.dk/io_uring.pdf), a new-ish IO framework for linux that requires pretty modern kernels
- [shared-nothing architecture](https://en.wikipedia.org/wiki/Shared-nothing_architecture), which I _think_ here means that the keys in the database are sharded to particular fibers so the program can avoid locks
	- > To solve this, we used [shared-nothing architecture](https://en.wikipedia.org/wiki/Shared-nothing_architecture), which allows us to partition the keyspace of the memory store between threads, so that each thread would manage its own slice of dictionary data.

note that it has a BSL license - Business Source License, which makes it not OSS, usable for playing around with but not for commercial work (without paying).


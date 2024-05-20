---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://tigerbeetle.com/blog/a-friendly-abstraction-over-iouring-and-kqueue/

>  Consider this tale of I/O and performance. We’ll start with blocking I/O, explore io_uring and kqueue, and take home an event loop very similar to some software you may find familiar. 

A really nice article where the authors, with not a lot of code, create a reasonably simple abstraction over io_uring on linux and kqueue on mac.

Mitchell Hashimoto took this sketch for an architecture and used it to create [libxev](https://github.com/mitchellh/libxev), which powers his (still unreleased) `ghostty` terminal.
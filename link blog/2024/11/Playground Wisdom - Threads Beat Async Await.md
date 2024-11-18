---
created: 2024-11-18T12:07:27.955Z
updated: 2024-11-18T12:07:27.955Z
---
https://lucumr.pocoo.org/2024/11/18/threads-beat-async-await/

 >The reason it's blocking is [because memory access can be blocking](https://huonw.github.io/blog/2024/08/async-hazard-mmap/)! You might not think of it this way, but there are many reasons why just touching a memory region can take time. The most obvious one is memory-mapped files. If you're touching a page that hasn't been loaded yet, the operating system will have to shovel it into memory before returning back to you. There is no “await touching this memory” expression, because if there were, we would have to await _everywhere_. That might sound petty but blocking memory reads were at the source of a series of incidents at Sentry [[1]](https://lucumr.pocoo.org/2024/11/18/threads-beat-async-await/#footnote-1).

> The trade-off that async/await makes today is that the idea is that not everything needs to block or needs to suspend. The reality, however, has shown me that many more things really want to suspend, and if a random memory access is a case for suspending, then is the abstraction worth anything?

- [Armin Ronacher](https://lucumr.pocoo.org/2024/11/18/threads-beat-async-await/)
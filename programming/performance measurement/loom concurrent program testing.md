---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://docs.rs/loom/latest/loom/

> Loom is a tool for testing concurrent programs.

> At a high level, it runs tests many times, permuting the possible concurrent executions of each test according to what constitutes valid executions under the [C11 memory model](https://en.cppreference.com/w/cpp/atomic/memory_order). It then uses state reduction techniques to avoid combinatorial explosion of the number of possible executions

> Testing concurrent programs is challenging; concurrent strands of execution can interleave in all sorts of ways, and each such interleaving might expose a concurrency bug in the program. Some bugs may be so rare that they only occur under a very small set of possible executions, and may not surface even if you run the code millions or billions of times.

> Loom provides a way to deterministically explore the various possible execution permutations without relying on random executions. This allows you to write tests that verify that your concurrent code is correct under _all_ executions, not just “most of the time”.
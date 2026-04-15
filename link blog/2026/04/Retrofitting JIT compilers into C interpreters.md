---
created: 2026-04-15T12:41:08.380Z
updated: 2026-04-15T12:41:08.380Z
---
https://tratt.net/laurie/blog/2026/retrofitting_jit_compilers_into_c_interpreters.html

Very cool work by Laurence Tratt, Edd Barrett, Lukas Diekmann, and Pavel Durov to create a system, `yk`, which accepts an interpreter for a language (lua or python for example) and emits a meta-tracing JIT compiler for it.

> [!info] the blog post explains what a _meta-tracing JIT_ is much better than I could here

The upshot of this is that you can, with a reasonable amount of work, automate the construction of  JIT compiler from an interpreter that doesn't natively support it.

Put another way, you can build a Pypy-like JIT interpreter from the regular C python interpreter, _automatically_.

The article does a great job of walking you through what all this means and how it does it. Very cool work!
---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/bazelbuild/starlark

Bazel's python subset configuration language. 

> Starlark (formerly known as Skylark) is a language intended for use as a configuration language. It was designed for the [Bazel](https://bazel.build/) build system, but may be useful for other projects as well. This repository is where Starlark features are proposed, discussed, and specified. It contains information about the language, including the [specification](https://github.com/bazelbuild/starlark/blob/master/spec.md). There are [multiple implementations of Starlark](https://github.com/bazelbuild/starlark/blob/master/users.md).

> Starlark is a dialect of [Python](https://www.python.org/). Like Python, it is a dynamically typed language with high-level data types, first-class functions with lexical scope, and garbage collection. Independent Starlark threads execute in parallel, so Starlark workloads scale well on parallel machines. Starlark is a small and simple language with a familiar and highly readable syntax. You can use it as an expressive notation for structured data, defining functions to eliminate repetition, or you can use it to add scripting capabilities to an existing application.

I really like projects that define design principles up front:

> Design Principles
> -   **Deterministic evaluation**. Executing the same code twice will give the same results.
> -   **Hermetic execution**. Execution cannot access the file system, network, system clock. It is safe to execute untrusted code.
> -   **Parallel evaluation**. Modules can be loaded in parallel. To guarantee a thread-safe execution, shared data becomes immutable.
> -   **Simplicity**. We try to limit the number of concepts needed to understand the code. Users should be able to quickly read and write code, even if they are not expert. The language should avoid pitfalls as much as possible.
> -   **Focus on tooling**. We recognize that the source code will be read, analyzed, modified, by both humans and tools.
> -   **Python-like**. Python is a widely used language. Keeping the language similar to Python can reduce the learning curve and make the semantics more obvious to users.
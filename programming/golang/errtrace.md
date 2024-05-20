---
updated: '2023-12-09T18:24:04Z'
created: '2023-12-09T18:24:04Z'
---
https://github.com/bracesdev/errtrace

> errtrace is an **experimental** package to trace an error's return path — the return trace — through a Go program.

> Where a stack trace tracks the code path that led to an error, a return trace tracks the code path that the error took to get to the user. Often these are the same path, but in Go they can diverge, since errors are values that can be transported across goroutines (e.g. with channels). When that happens, a return trace can be more useful than a stack trace.

> This library is inspired by [Zig's error return traces](https://ziglang.org/documentation/0.11.0/#Error-Return-Traces).

Neat idea! stack traces are so valuable but often obscure the actually useful data they present.
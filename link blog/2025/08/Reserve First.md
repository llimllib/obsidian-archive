---
created: 2025-08-19T11:20:58.154Z
updated: 2025-08-19T11:20:58.154Z
---
https://matklad.github.io/2025/08/16/reserve-first.html

> In these two cases in particular, the only source of errors is fallible allocation. And there’s a pattern to fix it:

> - First, _reserve_ enough memory for operation, without applying any changes to the data structure,
> - Then, mutate the data structure in an error-free code path.

This seems to me a very similar principle to the one presented in [[Parse, don't validate]] - to perform a potentially dangerous operation, do work up front to change the environment and make errors impossible later on.
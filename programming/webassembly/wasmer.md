---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://wasmer.io/

supports wasm in c#/C++/python/go/ruby/php/rust

still not _entirely_ clear on when I would use it. Two thoughts:

- I want some bit of functionality from Rust in Go or python
	- eg [this article](https://xeiaso.net/blog/carcinization-golang) that uses wasm to embed rust functionality in a go program
- Plugins
	- I could imagine a [[limbo]] written in go, where the plugins are provided as wasm-compiled bits of funcationality
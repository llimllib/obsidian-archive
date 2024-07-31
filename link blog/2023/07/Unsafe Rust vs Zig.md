---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://zackoverflow.dev/writing/unsafe-rust-vs-zig

> I wanted to... see how hard unsafe [[Rust]] would be by building a project that required a substantial amount of unsafe code.

> Then I would re-write the project in [[Zig]] to see if would be easier/better.

> After I finished both versions, I found that the Zig implementation was safer, faster, and easier to write. I’ll share a bit about building both and what I learned.

----

> **Unsafe Rust is hard**. A lot harder than C, this is because unsafe Rust has a lot of nuanced rules about undefined behaviour (UB) — thanks to the borrow checker — that make it easy to perniciously break things and introduce bugs.

----

> Apart from not having crazy UB like in unsafe Rust, Zig is a language that understands that you are going to be doing memory-unsafe things, so its designed and optimized around making that experience much better and less error prone.

----

Worth noting that the author was doing something that is explicitly in Zig's wheelhouse (custom allocation strategies) and outside of Rust's. That said, we're still trying to figure out where the wheelhouse of those two languages is, so it's a useful data point.

via [jqtrde](http://jqtrde.com/) on [github](https://github.com/jqtrde)
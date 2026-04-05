---
created: 2026-04-05T15:21:22.083Z
updated: 2026-04-05T15:21:22.083Z
---
https://www.mattkeeter.com/blog/2026-04-05-tailcall/

Matt Keeter continues his quest to implement performant [UXN CPUs](https://wiki.xxiivv.com/site/uxntal_reference.html).

Well-explained and thorough article about using the `become` operator in nightly rust (TIL) to create a tail-call interpreter, and compare it against his assembly backends on a few architectures.

He also points to [this Massey Meta Machine](https://github.com/wasm3/wasm3/blob/main/docs/Interpreter.md#m3-massey-meta-machine) writeup, where he learned about tail-call interpreters. See [[Beating the compiler]] for previous discussion of tail-call interpreters in discussion of a previous post by the same author.
---
created: 2025-11-03T13:54:11.939Z
updated: 2025-11-03T13:54:11.939Z
---
https://jyn.dev/build-system-tradeoffs

A nice consideration of the tradeoffs of some different build systems. Doesn't really propose anything concrete, but is something like a modern [[Build systems á la carte]]

The main concrete recommendation is:

> Writing build rules in a "normal" (but constrained) programming language, then serializing them to a build graph, has surprisingly few tradeoffs. I'm not sure why more build systems don't do this.

Suggesting that writing code to generate a [[Ninja]] graph is what they consider the current state of the art

via [lobste.rs](https://lobste.rs/s/uwyfpy/build_system_tradeoffs)
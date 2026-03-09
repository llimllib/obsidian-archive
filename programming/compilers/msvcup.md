---
created: 2026-02-15T14:19:40.863Z
updated: 2026-02-15T14:19:40.863Z
---
https://github.com/marler8997/msvcup

> A standalone tool for installing the MSVC toolchain and Windows SDK without Visual Studio.

An article about what prompted the design: https://marler8997.github.io/blog/fixed-windows/

> I’m not interested in being a human debugger for someone else’s installer. I want the MSVC toolchain to behave like a modern dependency: versioned, isolated, declarative.

> I spent a few weeks building an open source tool to make things better. It’s called msvcup. It’s a small CLI program. On good network/hardware, it can install the toolchain/SDK in a few minutes, including everything to cross-compile to/from ARM. Each version of the toolchain/SDK gets its own isolated directory. It’s idempotent and fast enough to invoke every time you build.

I don't ever use Windows, but someday I may have to build something for people who do, so I'm saving this for that day.
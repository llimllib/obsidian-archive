---
created: 2024-09-16T00:44:41.487Z
updated: 2024-09-16T00:44:41.487Z
---
https://github.com/allyourcodebase

A project to replace `make`/`config`/`cmake` etc scripts for some foundational unix libraries with a zig `build.zig` file instead.

> We package C/C++ projects for the Zig build system so that you can reliably compile (and cross-compile!) them with ease.

> This both provides convenience for users of the Zig compiler toolchain and also showcases to C/C++ project maintainers what a build.zig file for their project looks like.

Zig can build some libraries unpatched, just by importing them as a dependency and writing a `build.zig` file. 
- for example, [here](https://github.com/allyourcodebase/harfbuzz/blob/main/build.zig) is harfbuzz's build.zig file

Others, they have to fork and patch
- for example, [here is cpython](https://github.com/allyourcodebase/cpython) and [here is its build.zig](https://github.com/allyourcodebase/cpython/blob/main/build.zig)

It's notable that the `build.zig` files are extremely flat and almost entirely devoid of any logic. Mostly, they contain a list of the files to be built and a list of the feature flags available.
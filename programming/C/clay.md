---
created: 2024-12-20T19:13:45.018Z
updated: 2024-12-20T19:13:45.018Z
---
https://www.nicbarker.com/clay
https://github.com/nicbarker/clay

> **_Clay_** (short for **C Layout**) is a high performance 2D UI layout library.

### Major Features

> - Microsecond layout performance
> - Flex-box like layout model for complex, responsive layouts including text wrapping, scrolling containers and aspect ratio scaling
> - Single ~2k LOC **clay.h** file with **zero** dependencies (including no standard library)
> - Wasm support: compile with clang to a 15kb uncompressed **.wasm** file for use in the browser
> - Static arena based memory use with no malloc / free, and low total memory overhead (e.g. ~3.5mb for 8192 layout elements).
> - React-like nested declarative syntax
> - Renderer agnostic: outputs a sorted list of rendering primitives that can be easily composited in any 3D engine, and even compiled to HTML (examples provided)

Very neat UI library, including an HTML renderer such that it renders itself as a web page for the landing page.

via [news.yc](https://news.ycombinator.com/item?id=42463123)




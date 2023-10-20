https://github.com/ern0/howto-wasm-minimal

## Goals

-   use no Emscripten or any libs
-   simple toolchain, compile to wasm in a single step
-   wasm may use memory prepared by JavaScript
-   do something relative compute-intensive
-   do something visible

Found via [this tweet](https://twitter.com/simonw/status/1508505057976758275)

> Love this minimal WASM demo - code is in the linked GitHub repo, it uses WASM to run a tiny bit of C++ code that performs image processing (colour changes + an animated blur) against an image loaded onto a canvas element

and simon's notes on building and running it: https://til.simonwillison.net/webassembly/compile-to-wasm-llvm-macos
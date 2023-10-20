Salvatore Sanfilippo [asked on twitter](https://twitter.com/antirez/status/1569986950509088769) for recommendations for small javascript engines to embed in a program, and got a few:

## [duktape](https://duktape.org/)

> # Duktape
> Duktape is an **embeddable Javascript** engine, with a focus on **portability** and compact **footprint**.

> Duktape is easy to integrate into a C/C++ project: add `duktape.c`, `duktape.h`, and `duk_config.h` to your build, and use the Duktape API to call ECMAScript functions from C code and vice versa.

## [quickjs](https://bellard.org/quickjs/)

by Fabrice Bellard

> QuickJS is a small and embeddable Javascript engine. It supports the [ES2020](https://tc39.github.io/ecma262/) specification including modules, asynchronous generators, proxies and BigInt.

> It optionally supports mathematical extensions such as big decimal floating point numbers (BigDecimal), big binary floating point numbers (BigFloat) and operator overloading.

> Main Features:
> 
> -   Small and easily embeddable: just a few C files, no external dependency, 210 KiB of x86 code for a simple hello world program.
> -   Fast interpreter with very low startup time: runs the 75000 tests of the [ECMAScript Test Suite](https://github.com/tc39/test262) in about 100 seconds on a single core of a desktop PC. The complete life cycle of a runtime instance completes in less than 300 microseconds.
> -   Almost complete [ES2020](https://tc39.github.io/ecma262/) support including modules, asynchronous generators and full Annex B support (legacy web compatibility).
> -   Passes nearly 100% of the ECMAScript Test Suite tests when selecting the ES2020 features. A summary is available at [Test262 Report](https://test262.report/).
> -   Can compile Javascript sources to executables with no external dependency.
> -   Garbage collection using reference counting (to reduce memory usage and have deterministic behavior) with cycle removal.
> -   Mathematical extensions: BigDecimal, BigFloat, operator overloading, bigint mode, math mode.
> -   Command line interpreter with contextual colorization implemented in Javascript.
> -   Small built-in standard library with C library wrappers.

[Espruino](https://github.com/espruino/Espruino):

> Espruino is a JavaScript interpreter for microcontrollers. It is designed for devices with as little as 128kB Flash and 8kB RAM.
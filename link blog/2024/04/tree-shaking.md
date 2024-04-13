https://wingolog.org/archives/2023/11/24/tree-shaking-the-horticulturally-misguided-algorithm

> despite the hype, WebAssembly has had limited success on the web... WebAssembly has not been a Web success for DOM-heavy apps. Nobody is talking about rewriting the front-end of [wordpress.com](https://wordpress.com) in Wasm, for example

> Wasm has also not really been a success for languages that aren’t, like, C or Rust... One of the sticking points for this class of language. is that C#, for example, will want to ship with a garbage collector, and that it is annoying to have to do this.

> Happily, this restriction is going away, as all browsers are going to ship support for reference types and garbage collection within the next months

neat! I didn't know that.

> To recap: now that it supports GC, Wasm could be a winner for web development in Python and other languages. You would need a different toolchain and an effective tree-shaking algorithm, so that user experience does not degrade. So let’s talk about tree shaking!

The author then goes on to talk about the difficulties in tree-shaking languages that weren't built to be tree-shaken. They conclude:

> With GC, Wasm makes it thinkable to do DOM programming in languages other than JavaScript. It will only be feasible for mass use, though, if the resulting Wasm modules are small, and that means significant investment on each language’s toolchain. Often this will take the form of alternate toolchains that incorporate experimental tree-shaking algorithms, and whose alternate standard libraries facilitate the tree-shaker.
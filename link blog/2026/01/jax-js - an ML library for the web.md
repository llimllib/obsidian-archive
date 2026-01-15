---
created: 2026-01-06T19:56:09.440Z
updated: 2026-01-06T19:56:09.440Z
---
https://ss.ekzhang.com/p/jax-js-an-ml-library-for-the-web

> While the JavaScript JIT is really good, it’s not optimized for tight numerical loops. JavaScript doesn’t even have a fast, native integer data type! So how can you run fast numerical code on the web?

> The answer is to rely on new browser technologies — WebAssembly and WebGPU, which allow you to run programs at near-native speeds. WebAssembly is a low-level portable bytecode, and WebGPU is GPU shaders on the web.

> If we can use these native runtimes, then this lends itself to a programming model similar to JAX, where you _trace_ programs and _JIT_ _compile_ them to GPU kernels. Here, instead of Nvidia CUDA, we write pure JavaScript to generate WebAssembly and WebGPU kernels. Then we can run them and execute instructions at near-native speed, skipping the JavaScript interpreter bottleneck.

https://github.com/ekzhang/jax-js
https://jax-js.com


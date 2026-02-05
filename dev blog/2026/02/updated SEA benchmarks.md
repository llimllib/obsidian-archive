---
created: 2026-02-05T12:02:55.150Z
updated: 2026-02-05T12:02:55.150Z
---
Joyee Cheung [made the process to build a node executable much simpler](https://joyeecheung.github.io/blog/2026/01/26/improving-single-executable-application-building-for-node-js/), so I updated my [example repository](https://github.com/llimllib/node-esbuild-executable) that shows how to build a binary with node, bun, and deno with the new node instructions.

While I was at it, I updated the benchmark table with the latest version of each interpreter:

| interpreter | version | build (ms) | size (mb) | execution time   |
| ----------- | ------- | ---------- | --------- | ---------------- |
| node        | 25.6.0  | 3420       | 93        | 34.1 ms ± 0.9 ms |
| bun         | 1.3.8   | 600        | 57        | 18.6 ms ± 0.7 ms |
| deno        | 2.6.8   | 790        | 72        | 32.4 ms ± 0.5 ms 
The [benchmarked program](https://github.com/llimllib/node-esbuild-executable/blob/main/index.js) is an extremely simple program that uses a library, just to demonstrate how to compile something that uses one.

Read that [README](https://github.com/llimllib/node-esbuild-executable/blob/main/README.md) or [[Making a single-file executable with node and esbuild]] for more
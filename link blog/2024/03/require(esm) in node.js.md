https://joyeecheung.github.io/blog/2024/03/18/require-esm-in-node-js/

> Recently I landed experimental [support for `require()`-ing synchronous ES modules in Node.js](https://github.com/nodejs/node/pull/51977), a feature that has been long overdue. In the pull request, [I commented](https://github.com/nodejs/node/pull/51977#issuecomment-1994837735) with my understanding about why it did not happen sooner before this pull request in 2024. This post expands on that comment a bit more.

---

> Last year when I was browsing the V8 code [to fix a memory leak](https://joyeecheung.github.io/blog/2023/12/30/fixing-nodejs-vm-apis-2/), I found out by chance that ESM itself was not actually designed to be unconditionally asynchronous. Rather, it was designed to be only conditionally asynchronous - only when the graph contains top-level `await`.

> Then it would seem very natural for `require()` to at least support ESM graphs that contains no top-level `await`. While some libraries might have valid reasons to use top-level `await`, it’s probably not that common a thing - indeed, when I later tested my `require(esm)` PR on high-impact ESM-only packages in the npm registry, none of ~30 that I tested contained top-level `await` - and supporting synchronous modules in `require()` would probably already be enough to make a lot of headaches in the ecosystem go away.

The article has lots of interesting cultural observations about the node.js development process, and how scary it is to develop on controversial parts of the system in the open.
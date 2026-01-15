---
created: 2025-10-29T18:17:41.687Z
updated: 2025-10-29T18:17:41.687Z
---
https://github.com/tinysearch/tinysearch
https://endler.dev/2019/tinysearch

> tinysearch is a lightweight, fast, full-text search engine. It is designed for static websites.

> tinysearch is written in Rust, and then compiled to WebAssembly to run in a browser.  
It can be used together with static site generators such as [Jekyll](https://jekyllrb.com/), [Hugo](https://gohugo.io/), [Zola](https://www.getzola.org/), [Cobalt](https://github.com/cobalt-org/cobalt.rs), or [Pelican](https://getpelican.com).

> tinysearch is a Rust/WASM port of the Python code from the article ["Writing a full-text search engine using Bloom filters"](https://www.stavros.io/posts/bloom-filter-search-engine/). It can be seen as an alternative to [lunr.js](https://lunrjs.com/) and [elasticlunr](http://elasticlunr.com/), which are too heavy for smaller websites and load a lot of JavaScript.

> Under the hood it uses a [Xor Filter](https://arxiv.org/abs/1912.08258) — a datastructure for fast approximation of set membership that is smaller than bloom and cuckoo filters. Each blog post gets converted into a filter that will then be serialized to a binary blob using [bincode](https://github.com/bincode-org/bincode). Please note that the underlying technologies are subject to change.

Only finds entire words, so not suitable for my usage on this site
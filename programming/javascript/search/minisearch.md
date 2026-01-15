---
updated: 2025-10-29T18:33:53.142Z
created: 2024-03-22T20:51:34Z
---
https://github.com/lucaong/minisearch/

> `MiniSearch` is a tiny but powerful in-memory fulltext search engine written in JavaScript. It is respectful of resources, and it can comfortably run both in Node and in the browser.

> `MiniSearch` addresses use cases where full-text search features are needed (e.g. prefix search, fuzzy search, ranking, boosting of fields…), but the data to be indexed can fit locally in the process memory. While you won't index the whole Internet with it, there are surprisingly many use cases that are served well by `MiniSearch`. By storing the index in local memory, `MiniSearch` can work offline, and can process queries quickly, without network latency.

I ended up using this for [this sites' search function](https://notes.billmill.org/search.html) after being unhappy with the results from both [[FlexSearch]] and [[Fuse]], and I'm happy enough with it. The code for it is [here](https://github.com/llimllib/obsidian_notes/blob/36e9ba27cf47a53c9cf46f4a016b2d00294a93f3/templates/search.html#L23-L98) if you want to see what a usage of the library looks like

see also: [[FlexSearch]] [[pagefind]] [[Fuse]]
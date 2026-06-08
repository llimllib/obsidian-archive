---
created: 2026-06-08T01:41:20.781Z
updated: 2026-06-08T01:41:20.781Z
---
https://performance.dev/how-is-linear-so-fast-a-technical-breakdown

- They use a sync engine such that user changes are optimistically applied
- They carefully load only the JS/CSS that is required at the start, and preload as much as possible
- They chunk the application very granularly, and use a service worker to preload chunks

This made me interested in how their sync engine works, so I'm watching this talk:

<iframe width="560" height="315" src="https://www.youtube.com/embed/Wo2m3jaJixU?si=FLhcjMF6M6dWc8Dc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>\

- I've previously mentioned [[electric]], which implements a sync engine with CRDTs
- I've previously mentioned Replicache in [[Offline-First Landscape]] and [[Real-time Collaboration with replicache and fly-replay]]
	- a news.yc commenter points to [this doc](https://doc.replicache.dev/concepts/how-it-works) about how replicache works
	- zero, who I guess are the company that supports replicache, have [this doc](https://zero.rocicorp.dev/docs/when-to-use#alternatives) which points to alternatives to it
- news.yc points to [this reverse-engineering](https://github.com/wzhudev/reverse-linear-sync-engine/blob/main/SUMMARY.md) of the linear sync engine
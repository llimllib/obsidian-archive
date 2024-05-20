---
updated: '2023-11-09T14:54:44Z'
created: '2023-11-09T14:54:44Z'
---
https://www.npmjs.com/package/blocked-at

> Detects slow synchronous execution and reports where it started.

gives a stack trace for every function that takes over the configured blocking threshold

According to [this article](https://www.ashbyhq.com/blog/engineering/detecting-event-loop-blockers), the async hooks mechanism is extremely slow so you may prefer to try [[blocked]]
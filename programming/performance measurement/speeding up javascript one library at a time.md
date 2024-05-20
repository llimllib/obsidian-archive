---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://marvinh.dev/blog/speeding-up-javascript-ecosystem/

Nice post showing how the author used flame graphs to find performance problems in some common JS libraries, and removed them (mainly by preventing unnecessary type conversions (which cause allocations))

mentioned [[speedscope]], which is a really handy tool
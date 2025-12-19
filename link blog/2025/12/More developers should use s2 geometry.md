---
created: 2025-12-19T14:10:38.275Z
updated: 2025-12-19T14:10:38.275Z
---
[Brandon Liu writes](https://go.bsky.app/redirect?u=https%3A%2F%2Fbdon.org%2F2025%2F12%2F19%2Fs2-geometry):

> [[s2 geometry|S2]] fits a sweet spot for indexing spatial data, not visualization or aggregate statistics. The Google reference implementation is in C++, which makes it difficult to use for web maps. Enter Peter Johnson’s [s2js](https://github.com/missinglink/s2js), a from-scratch implementation of S2 Geometry in pure JavaScript, with most major features such as RegionCoverer and boolean operations.

They link to a neat [demo app](https://bdon.github.io/s2js-demos/) where you draw a rectangle or polygon on a map, and it breaks it down into sub-regions using the s2 algorithm.
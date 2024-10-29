---
created: 2024-10-29T23:12:19.175Z
updated: 2024-10-29T23:12:19.175Z
---
https://www.timescale.com/blog/vector-databases-are-the-wrong-abstraction/

> embeddings are mistakenly treated as standalone data atoms that developers must manage rather than what they truly are: **derived data**. After all, [vector embeddings are high-dimensional representations of their source data](https://www.timescale.com/blog/a-beginners-guide-to-vector-embeddings/), whether the source data be text, images, or something else. There is a fundamental connection between the vector embedding and the source data it is generated from.

> When we reconceptualize embeddings as derived data, the absurdity of the current vector database abstraction becomes evident, with embeddings disconnected from their source data.

Makes sense to me, though my work with vector databases has only been tangential so far.
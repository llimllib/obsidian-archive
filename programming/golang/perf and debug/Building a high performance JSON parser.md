https://dave.cheney.net/high-performance-json.html

Superb walkthrough from Dave Cheney on building a [JSON parser](https://github.com/pkg/json) that's faster than the standard library parser, mainly by improving the API to return subslices of the input instead of allocating new objects.

Found via [this article](https://www.cockroachlabs.com/blog/high-performance-json-parsing/) about improving JSON performance in [[CockroachDB]]
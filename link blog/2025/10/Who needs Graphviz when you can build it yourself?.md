---
created: 2025-10-29T11:02:42.823Z
updated: 2025-10-29T11:02:42.823Z
---
https://spidermonkey.dev/blog/2025/10/28/iongraph-web.html

The author wasn't satisfied with graphviz's output for their compiler's graphs, so they studied out the `dot` layout algorithm and realized that they could tailor it for their own needs and produce something better

> Most graph layout algorithms are optimization problems, where error is minimized on some chosen metrics. However, these metrics seem to correlate poorly to readability in practice. For example, it seems good in theory to rearrange nodes to minimize edge crossings. But a predictable order of nodes seems to produce more sensible results overall, and simple rules for edge routing are sufficient to keep things tidy. (As a bonus, this also gives us layout stability from pass to pass.) Similarly, layout rules like “align parents with their children” produce more readable results than “minimize the lengths of edges”.

> Furthermore, by rejecting the optimization problem, a human author gains more control over the layout. We are able to position nodes “inside” of loops, and push post-loop content down in the graph, _because_ we reject this global constraint-solver approach. Minimizing “error” is meaningless compared to a human _maximizing_ meaning through thoughtful design.

> And finally, the resulting algorithm is simply more efficient. All the layout passes in iongraph are easy to program and scale gracefully to large graphs because they run in roughly linear time. It is better, in my view, to run a fixed number of layout iterations according to your graph complexity and time budget, rather than to run a complex constraint solver until it is “done”.

Source code [here](https://github.com/mozilla-spidermonkey/iongraph)
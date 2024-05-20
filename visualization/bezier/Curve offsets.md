---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
I wrote [an article](https://billmill.org/sol_1136.html) about drawing a curve with offsets. Some references:

[curve offsetting](https://pomax.github.io/bezierinfo/#offsetting)
[Tiller-Hanson algorithm explanation](https://math.stackexchange.com/questions/465782/control-points-of-offset-bezier-curve/467038#467038)
[wiki on parallel curves](https://en.wikipedia.org/wiki/Parallel_curve)

Recently I came across [this article](http://lin-ear-th-inking.blogspot.com/2022/01/jts-offset-curves.html), which presents a new-to-me algorithm for drawing offset curves that I can't say I fully grasp, but appears to give pretty nice results. It's in JTS, which is a Java library for dealing with vector geometry.

The pull request that adds it is here: https://github.com/locationtech/jts/pull/810
The GEOS pull request to port it is here: https://github.com/libgeos/geos/pull/530
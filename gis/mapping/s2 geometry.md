https://s2geometry.io/

> S2 is a library for spherical geometry that aims to have the same robustness, flexibility, and performance as the very best planar geometry libraries.

From the very useful https://s2geometry.io/about/overview

> Why not project onto an ellipsoid? (The Earth isn’t quite ellipsoidal either, but it is even closer to being an ellipsoid than a sphere.) The answer relates to the other goals stated above, namely performance and robustness. Ellipsoidal operations are still orders of magnitude slower than the corresponding operations on a sphere. Furthermore, robust geometric algorithms require the implementation of exact geometric predicates that are not subject to numerical errors. While this is fairly straightforward for planar geometry, and somewhat harder for spherical geometry, it is not known how to implement all of the necessary predicates for ellipsoidal geometry.

appears to be (unoficially?) from google. Related to [[h3 geometry]]
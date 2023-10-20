https://en.wikipedia.org/wiki/Jump_flooding_algorithm

> The **jump flooding algorithm** (**JFA**) is a [flooding algorithm](https://en.wikipedia.org/wiki/Flooding_algorithm "Flooding algorithm") used in the construction of [Voronoi diagrams](https://en.wikipedia.org/wiki/Voronoi_diagram "Voronoi diagram") and [distance transforms](https://en.wikipedia.org/wiki/Distance_transform "Distance transform")

> The JFA has desirable attributes in [GPU](https://en.wikipedia.org/wiki/GPU "GPU") computation, notably constant-time performance. However, it is only an approximate algorithm and does not always compute the correct result for every pixel, although in practice errors are few and the magnitude of errors is generally small

via [this news.yc discussion](https://news.ycombinator.com/item?id=36049386) of a [nice post](https://shaneosullivan.wordpress.com/2023/05/23/instant-colour-fill-with-html-canvas/) from the author of the neat [kidz fun art](https://www.kidzfun.art/?b=1685394930306) that they coded for their kids. (situated software!)

[here's an implementation of JFA on observable](https://observablehq.com/@rreusser/gpu-voronoi-diagrams-using-the-jump-flooding-algorithm) with some knobs you can turn


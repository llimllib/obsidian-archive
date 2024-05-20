---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/jbaileyh/geogrid

> Recent functionality for representing US states, European countries and World countries in a grid has been made available for ggplot2 [here](https://hafen.github.io/geofacet/) and there are many other great examples of **hand-specified** or **bespoke** grids. The challenge with this is that if you have a less commonly used geography then it might be hard to find a **hand-specified** or **bespoke** grid for your area of interest.

> What I wanted to do with `geogrid` is make it easier to generate these grids in ways that might be visually appealing and then assign the original geographies to their gridded counterparts in a way that made sense. Using an input of geospatial polgyons `geogrid` will generate either a regular or hexagonal grid, and then assign each of the polygons in your original file to that new grid.

Uses the [hungarian algorithm](https://en.wikipedia.org/wiki/Hungarian_algorithm), which I'll be honest I don't understand what it is or how it applies here
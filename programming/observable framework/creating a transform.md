---
updated: '2024-03-02T13:18:55Z'
created: '2024-03-02T13:18:55Z'
---
The [documentation](https://observablehq.com/plot/features/transforms#custom-transforms) is a little skimpy on this.
- the [Plot.transform](https://observablehq.com/plot/features/transforms#transform) function
- Fil's [loess transform](https://observablehq.com/@observablehq/plot-loess-168)
- Fil's [regression demo](https://observablehq.com/@fil/plot-regression)
- Fil's [normalizeMaxY](https://observablehq.com/@fil/plot-splom#normalizeMaxY) transform

Here's a no-op transform function that accepts `x` and `y` parameters:

```js
function noop({ x, y, ...options }) {
  return {
    ...Plot.transform(options, (data, facets, options) => {
      return { data, facets };
    }),
    x: x,
    y: y,
    ...options,
  };
}
```

You can call it like:

```js
Plot.plot({
  marks: [Plot.line(someData, noop({ x: "alpha", y: "beta" }))],
});
```
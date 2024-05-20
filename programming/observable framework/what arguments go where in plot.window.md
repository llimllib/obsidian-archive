---
updated: '2024-03-02T20:46:32Z'
created: '2024-03-02T20:00:44Z'
---
From the [documentation of windowY](https://observablehq.com/plot/transforms/window#windowY):

> windowY(_k_, _options_)
```js
Plot.windowY(24, {x: "Date", y: "Anomaly"})
```

it seems like the first argument is a value of `k`, and the second is a list of options. Earlier in the document, it gives a list of [window options](https://observablehq.com/plot/transforms/window#window-options)

But if you try to use those window options in the second argument, like for example:

```js
Plot.windowY(10, {
  anchor: "end",
  reduce: "sum",
  x: "x",
  y: "y",
}),
```

You'll be confused; there are no errors, `x` and `y` work as expected, but `reduce` and `anchor` will be ignored.

It took me a while to figure out that the first argument to `windowY` is in fact a value for `k` **or** an options argument, which take the options given in the  [window options](https://observablehq.com/plot/transforms/window#window-options) documentation above. So `windowY` really is:

> windowY(int|options, options)

Where the **first** `options` argument takes the window options linked above. The **second** options argument takes a set of arguments that are, I believe, returned directly to the calling function.

Extra confusingly, it seems that you can put the `x` and `y` properties in _either_ options hash, and they will work.

Looking at the Typescript types for the function helps clarify it:

```typescript
export function windowY<T>(options?: T & WindowOptions): Transformed<T>;
export function windowY<T>(windowOptions?: WindowOptions | WindowOptions["k"], options?: T): Transformed<T>;
```

the first options object can be the union of `T` and `WindowOptions`, where `T` (I think) is the type of the options hash for the parent object of windowY(?). Alternately, in the two hash form, you can pass window options (or `k` directly) as the first argument, and options to be returned as the second argument.

In fact, you may even want to pass different arguments with the same name to the first options object and the second one, so they can't be unified. `fil` gives this example:

```js
Plot.map(
  { y: Plot.window(24), stroke: Plot.window(24) },
  { x: "date", y: "heartRate", stroke: "heartRate", z: null }
)
```

Where we pass `Plot.window(24)` as the y argument to the first options argument? I do not understand why though.

It seems to me this would be greatly clarified if it only accepted a single options hash.

I thought about editing the docs, but it seems like heavy work? Maybe I will give it a try.
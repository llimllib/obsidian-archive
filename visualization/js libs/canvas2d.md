---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
Interesting article on new features for canvas:

https://developer.chrome.com/blog/canvas2d/

especially interesting are `ctx.reset()` and filters:

```js
  ctx.filter = new CanvasFilter([    
    {filter: "gaussianBlur", stdDeviation: 5},    
    {filter: "convolveMatrix",
	 kernelMatrix: [
	    [-3, 0, 0],
        [0, 0.5, 0],
        [0, 0, 3]]
    },
    {filter: "colorMatrix", type: "hueRotate", values: 90},
  ]);
```

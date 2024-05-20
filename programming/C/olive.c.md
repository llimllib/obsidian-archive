---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/tsoding/olive.c

> Simple graphics library that does not have any dependencies and renders everything into the given memory pixel by pixel. Visit [https://tsoding.org/olive.c/](https://tsoding.org/olive.c/) to see some demos.

[Here's an example](https://github.com/tsoding/olive.c/blob/master/demos/triangle.c) that renders a rotating triangle and a rotating circle, with a comment that helps explain the motivation:

```c
// This example renders a rotating triangle.
// This idea is that you can take this code and compile it to different platforms with different rendering machanisms:
// native with SDL, WebAssembly with HTML5 canvas, etc.
```
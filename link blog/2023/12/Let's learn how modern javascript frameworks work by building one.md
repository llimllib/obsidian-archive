---
updated: '2023-12-03T21:39:09Z'
created: '2023-12-03T21:39:09Z'
---
https://nolanlawson.com/2023/12/02/lets-learn-how-modern-javascript-frameworks-work-by-building-one/

- how to build DOM elements quickly
	- create them in a `template` element and then clone them:
	```
	const template = document.createElement('template')
    template.innerHTML = `
      <div class="blue">Blue!</div>
    `
    template.content.cloneNode(true) // this is fast!
    ```
- `queueMicrotask`
	- https://developer.mozilla.org/en-US/docs/Web/API/queueMicrotask
	- > The **`queueMicrotask()`** method, which is exposed on the [`Window`](https://developer.mozilla.org/en-US/docs/Web/API/Window) or [`Worker`](https://developer.mozilla.org/en-US/docs/Web/API/Worker) interface, queues a microtask to be executed at a safe time prior to control returning to the browser's event loop.
	- `queueMicrotask(() => doSomething())` is very similar to `doSomething().resolve().then()`

Lots more neat stuff, though some of it is a bit over my head.
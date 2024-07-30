---
created: 2024-07-30T13:34:33.168Z
updated: 2024-07-30T13:34:33.168Z
---
https://github.com/snabbdom/snabbdom

> Virtual DOM is awesome. It allows us to express our application's view as a function of its state. But existing solutions were way too bloated, too slow, lacked features, had an API biased towards OOP , and/or lacked features I needed.

> Snabbdom consists of an extremely simple, performant, and extensible core that is only ≈ 200 SLOC. It offers a modular architecture with rich functionality for extensions through custom modules. To keep the core simple, all non-essential functionality is delegated to modules.

Used by [[lichess]]; they replaced mithril with it.

Sample from their readme:

```js
import {
  init,
  classModule,
  propsModule,
  styleModule,
  eventListenersModule,
  h
} from "snabbdom";

const patch = init([
  // Init patch function with chosen modules
  classModule, // makes it easy to toggle classes
  propsModule, // for setting properties on DOM elements
  styleModule, // handles styling on elements with support for animations
  eventListenersModule // attaches event listeners
]);

const container = document.getElementById("container");

const vnode = h(
  "div#container.two.classes",
  { on: { click: () => console.log("div clicked") } },
  [
    h("span", { style: { fontWeight: "bold" } }, "This is bold"),
    " and this is just normal text",
    h("a", { props: { href: "/foo" } }, "I'll take you places!")
  ]
);
// Patch into empty DOM element – this modifies the DOM as a side effect
patch(container, vnode);

const newVnode = h(
  "div#container.two.classes",
  { on: { click: () => console.log("updated div clicked") } },
  [
    h(
      "span",
      { style: { fontWeight: "normal", fontStyle: "italic" } },
      "This is now italic type"
    ),
    " and this is still just normal text",
    h("a", { props: { href: "/bar" } }, "I'll take you places!")
  ]
);
// Second `patch` invocation
patch(vnode, newVnode); // Snabbdom efficiently updates the old view to the new state
```
---
updated: '2024-01-17T15:31:06Z'
created: '2024-01-17T15:31:06Z'
---
https://timkellogg.me/blog/2024/01/17/htmx

> I wrote an [HTMX](https://htmx.org/) app and it was easy to develop a powerful plugin system within it. That surprised me. I had assumed that JSON-driven REST APIs were the only way to make composable web APIs. In my mind, HTMX blends the backend and frontend together into one monolithic component. It seemed counterintuitive.

---

> the combination of React + an API isn’t just monolithic, it’s a monolith split across a _distributed system_. And those are **extremly non-composable**.

> Individual React components are very composable. But when you combine the requirements that I need, spanning the full stack, you find yourself in what I like to describe as a distributed system, since state is split between the client and server.

> ...it feels like the HTML is more like a configuration language, with instructions for how all the pieces fit together. There is state, but it’s hidden within the engine that interprets my declarative configuration (a.k.a the browser).
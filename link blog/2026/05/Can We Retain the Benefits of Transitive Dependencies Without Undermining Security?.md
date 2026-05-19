---
created: 2026-05-19T02:50:11.599Z
updated: 2026-05-19T02:50:11.599Z
---
> let me outline where I would one day like our software to go. I would like to run software, built from multiple components (i.e. dependencies of some kind), in such a way that:

> 1. Components are isolated from each other as much as possible.
> 2. Each component only has the minimum permissions it needs.

> For example, I don’t want my image decoding component to have network access, or the ability to access RAM with passwords in; but I do want my network downloading component to have network access, and I do want to be able to create a component that can manage and use passwords...

> In other words, I want to split software up into mutually distrusting dynamic “cells”, like processes, but with the ability to communicate more easily, frequently, and cheaply. The communications between dynamic components would need to be tightly specified, and if a component fails to communicate in exactly the required way, other components should ignore all interactions.

- [Lawrence Tratt](https://tratt.net/laurie/blog/2024/can_we_retain_the_benefits_of_transitive_dependencies_without_undermining_security.html)
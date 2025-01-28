---
created: 2025-01-28T13:29:17.195Z
updated: 2025-01-28T13:29:17.195Z
---
https://tratt.net/laurie/blog/2024/can_we_retain_the_benefits_of_transitive_dependencies_without_undermining_security.html

> With that qualification in mind, let me outline where I would one day like our software to go. I would like to run software, built from multiple components (i.e. dependencies of some kind), in such a way that:

> 1. Components are isolated from each other as much as possible.
> 2. Each component only has the minimum permissions it needs.

> For example, I don’t want my image decoding component to have network access, or the ability to access RAM with passwords in; but I do want my network downloading component to have network access, and I do want to be able to create a component that can manage and use passwords.

I don't actually love his vision for components bound by capabilities, but I am glad that some people are still blogging about the ways we might change computing for the better.
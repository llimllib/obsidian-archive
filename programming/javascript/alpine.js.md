https://alpinejs.dev

> Alpine is a rugged, minimal tool for composing behavior directly in your markup. Think of it like jQuery for the modern web. Plop in a script tag and get going.

Seems to have a similar aesthetic to [[programming/htmx/htmx]], but to deal with client-side JS instead of server interaction. There are several projects that mix the two.

Tries to be so small that you don't need to webpack-ify, you just include it and move forward jquery-style

---
news.yc comments:

> I'm glad alternatives like Alpine exist for small sites that don't need many additional behaviours. But having used Alpine for a medium-sized art gallery website last year, I can't really recommend it for anything larger than a very simple site. The fact that all your code is scattered as strings everywhere without error checking or types makes it really hard to debug and work with long-term...
> For lightweight front-end tooling, nothing has unseated the ease of Preact for me.

---

> I find the sweet spot for utility frameworks like AlpineJS is when used in conjunction with server-side components

Interesting idea for pushup!
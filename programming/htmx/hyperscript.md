---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://hyperscript.org/

Hyperscript is a scripting language for doing front end web development. It is designed to make it very easy to respond to events and do simple DOM manipulation in code that is directly embedded on elements on a web page.

Example

```html
<button _="on click toggle .red on me">
Click Me
</button>
```

> The first thing to notice is that hyperscript is defined _directly on the button_, using the `_` (underscore) attribute.

 >The next thing you will notice about hyperscript is its syntax, which is very different than most programming languages used today. Hyperscript is part of the [xTalk](https://en.wikipedia.org/wiki/XTalk) family of scripting languages, which ultimately derive from [HyperTalk](https://hypercard.org/HyperTalk%20Reference%202.4.pdf). These languages all read more like english than the programming languages you are probably used to.

> This unusual syntax has advantages, once you get over the initial shock:

> -   It is very distinctive, making it obvious when hyperscript is being used in a web page
> -   It is very easy to read, making it obvious what a script is doing

From the authors of [[programming/javascript/HTMX]]
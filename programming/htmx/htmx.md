previously [[programming/javascript/HTMX]]

https://htmx.org/

> htmx gives you access to [AJAX](https://htmx.org/docs#ajax), [CSS Transitions](https://htmx.org/docs#css_transitions), [WebSockets](https://htmx.org/docs#websockets) and [Server Sent Events](https://htmx.org/docs#sse) directly in HTML, using [attributes](https://htmx.org/reference#attributes), so you can build [modern user interfaces](https://htmx.org/examples) with the [simplicity](https://en.wikipedia.org/wiki/HATEOAS) and [power](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm) of hypertext

The idea as I understand it (i.e. minimally) is that instead of using javascript you can render templated HTML on the server side and send them over the wire where they can be dynamically inserted, creating an SPA-like app with less hassle.

I'm probably misunderstanding though, to research.

via https://edofic.com/posts/2022-01-28-low-js/, though I've seen it before

-----
https://nomadiq.hashnode.dev/reimagining-front-end-web-development-with-htmx-and-hyperscript

> In recent years, a few mavericks and renegades have started to turn away from the world of JS frameworks and the inevitable bloated _node_modules_ folders. But what if you want a smooth single-page app experience, rather than waiting for the whole page to render every time you click a button? Of course, nobody wants to write a load of boilerplate JS for every little interaction. This is where _hypermedia_ in the form of [htmx](https://htmx.org/) and [hyperscript](https://hyperscript.org/) come in.

------------

https://htmx.org/essays/hypermedia-driven-applications/

> Following the REST notion of architectural [constraints](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm), two such constraints characterize the HDA (Hypermedia-Driven Architecture) architecture:

> -   An HDA uses _declarative, HTML-embedded syntax_ rather than imperative scripting to achieve better front-end interactivity
> -   An HDA interacts with the server **in terms of hypermedia** (i.e. HTML) rather than a non-hypermedia format (e.g. JSON)

> By adopting these two constraints, the HDA architecture stays within the original [REST-ful](https://developer.mozilla.org/en-US/docs/Glossary/REST) architecture of the web in a way that the SPA architecture does not.

> In particular, HDAs continue to use [Hypermedia As The Engine of Application State (HATEOAS)](https://htmx.org/essays/hateoas/), whereas most SPAs abandon HATEOAS in favor of a client-side model and data (rather than hypermedia) APIs.

Essay on the proper use, application, and aesthetics of, HDA applications

Has useful code examples
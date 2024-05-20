---
updated: '2023-12-28T05:14:16Z'
created: '2023-12-28T05:14:16Z'
---
https://bvisness.me/luax/

> This website now runs on a custom language called **LuaX**.

> It’s like JSX, but for Lua. You just write a Lua file that returns a chunk of HTML. You can compose more interesting pages by writing functions that return HTML.

...

> It feels like we’ve regressed. 15 years ago it was fine to run a script from scratch on every single request, but today we insist that we have to serve every personal website from a CDN. That means no fun allowed—if you so much as want the ©2023 in the footer to update, you’ll need to rebuild and redeploy the site.

> I don’t want that. I want my ©2023 to update dynamically, dammit.

...

> I have tried so many template languages over the years. I’ve used [mustache](https://mustache.github.io/), [Liquid](https://jekyllrb.com/docs/liquid/), [nunjucks](https://mozilla.github.io/nunjucks/), [Blade](https://laravel.com/docs/5.0/templates), [Django](https://docs.djangoproject.com/en/1.11/ref/templates/), and of course [Go templates](https://pkg.go.dev/text/template) (commonly seen in systems like [Hugo](https://gohugo.io/)).

> ...Just like the C preprocessor, these template languages are not real languages. They are inflexible and inextensible. The few tools they provide for reuse and composition are incredibly weak. And just like C macros, these languages aren’t powerful enough to manipulate the data they’re given, only to blindly spit it back out.

> ...This is why JSX is so much better. Instead of JS-inside-HTML, it’s HTML-inside-JS. It flips the ownership around. When you need to do something interesting, you don’t need to learn some underpowered language, or contort your work to fit a broken system, or remember which escaping functions to use. You just _write code_ and the rest sorts itself out.

...

So he ported the lua parser to go, and modified it to include his own JSX-alike!

> What I wanted was something I could embed easily in an existing app. Lua fit the bill nicely. But even more importantly, Lua is _extremely_ easy to parse. The [entire language grammar](https://www.lua.org/manual/5.1/manual.html#8) fits on one screen, and the [official parser](https://www.lua.org/source/5.1/lparser.c.html) is less than 1500 lines of code. Furthermore, Lua didn’t use `<` for anything except comparisons, so there was no ambiguity—HTML tags could be used wherever tables were used.

> It was therefore very easy to create a custom recursive descent parser. I mostly just ported the official parser to Go, and modified `parseSimpleExp` to parse tags as well as tables.

> ...The [end result](https://github.com/bvisness/bvisness.me/blob/2719c40e620f5721801758d4d4e6714abfaabc2b/bhp/transpile.go) is less than 1000 lines of code. About 700 of them are just parsing Lua, with the remaining ~300 being used for my new features. And it took me only a couple days!

Lovely, lovely stuff. Clear thinking and bold action.
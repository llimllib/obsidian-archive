---
created: 2026-01-12T14:29:23.475Z
updated: 2026-01-12T14:29:23.475Z
---
https://martinalderson.com/posts/which-programming-languages-are-most-token-efficient/

The author found a nice simple way to answer the question: measure the token count for [Rosetta Code](https://rosettacode.org/wiki/Rosetta_Code) [problems](https://rosettacode.org/wiki/Category:Programming_Tasks) which have solutions in all the languages they were interested in.

Short and thoughtful blog.

> There was a very meaningful gap of 2.6x between C (the least token efficient language I compared) and Clojure (the most efficient).

> Unsurprisingly, dynamic languages were much more token efficient (not having to declare _any_types saves a lot of tokens) - though JavaScript was the most verbose of the dynamic languages analysed.

> What did surprise me though was just _how_ token efficient some of the functional languages like Haskell and F# were - barely less efficient than the most efficient dynamic languages.

- Martin Alderson

via [mjd](https://elk.zone/hachyderm.io/@mjd@mathstodon.xyz/115882539937701535) in re [this github blog post](https://github.blog/ai-and-ml/llms/why-ai-is-pushing-developers-toward-typed-languages/), which includes one of my least-favorite argument styles:

> ## Is type safety that big of a deal?

> Yes!

> Next question.

It feels contemptuous of any reader who might have a different opinion. It's totally okay to decide not to legislate this question in every article about type-safe programming (or dynamic programming!) but please for the love of your readers, don't patronize them.
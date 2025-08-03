---
created: 2025-08-03T19:58:08.811Z
updated: 2025-08-03T19:58:08.811Z
---
https://lexi-lambda.github.io/blog/2019/11/05/parse-don-t-validate/

I've read this before, but it came up [on lobste.rs](https://lobste.rs/s/uon7sc/parse_don_t_validate_2019) and it had been a long while.

I would summarize the author's thesis as "instead of checking that data is valid, parse it into a data structure that must be valid, as soon as possible". It's a type-system-oriented view, but if you can implement it, you can make the interior of systems much simpler as they no longer have to consider the possibility that a value is invalid - it has already been parsed and proved to be valid.

> Consider: what is a parser? Really, a parser is just a function that consumes less-structured input and produces more-structured output. By its very nature, a parser is a partial function—some values in the domain do not correspond to any value in the range—so all parsers must have some notion of failure. Often, the input to a parser is text, but this is by no means a requirement, and `parseNonEmpty` is a perfectly cromulent parser: it parses lists into non-empty lists, signaling failure by terminating the program with an error message...

> [The] world doesn’t speak in product and sum types, but in streams of bytes, so there’s no getting around a need to do some parsing. Doing that parsing up front, before acting on the data, can go a long way toward avoiding many classes of bugs

I find this pattern useful in a more broad and metaphorical sense too: _shape the world,_ **then** _act on it_

If you look for an opportunity, you will sometimes find that you have an opportunity to do work up front to rearrange your data such that the system that acts on it can be simplified a great deal.
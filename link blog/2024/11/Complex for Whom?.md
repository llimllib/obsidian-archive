---
created: 2024-11-13T13:20:28.895Z
updated: 2024-11-13T13:20:28.895Z
---
> Rarely, if ever, do we talk about complexity within its rightful context – complexity **for whom**. Is a solution complex because it’s complex for the end user? Is it complex if it’s complex for an API consumer? Is it complex if it’s complex for the person maintaining the API service? Is it complex if it’s complex for someone outside the team maintaining it to understand?

- [Paul Tagliamonte](https://notes.pault.ag/complex-for-whom/)

This is something I think about constantly. Once you get the feel for it, you can start thinking intentionally about how you want to push around complexity, where it ought to live.

That's much more liberating than thinking only about eliminating it.

This quote also came up on my feed this morning, I guess it's Complexity Day:

> "Fools ignore complexity. Pragmatists suffer it. Some can avoid it. Geniuses remove it."—Dr. Alan J. Perlis, "Perlisisms: Epigrams in Programming" (1982)

via [raganwald](https://elk.zone/hachyderm.io/@raganwald@social.bau-ha.us/113475762215843545), who writes:

> We build up libraries of patterns to manage and sanitize problems rather than lifting our point of view and removing the problems.

I think programmers torture themselves with this! The constant pursuit of _the perfect abstraction_ in the hope of removing complexity causes programmers to add accidental complexity more often than it causes them to come up with "the genius stroke" that eliminates it in a poof of logic.

More often than not, I think we'd do better to accept the complexity, be happy with it, and move it somewhere that is clear and simple.

What is simple complexity?

I think of it like the 500-line switch statement that lives at the heart of many programs; it's a place where it's clear that the complexity lives, a place that needs to be coded efficiently and with painful clarity.

Instead of adding abstraction in the hopes of eliminating complexity, consider instead removing abstraction and laying your complexity out as simply and clearly as you can, in as few places as you can.

It's not always the right answer, but it's a pattern that's worth considering. Consider this your [Oblique Strategy](https://en.wikipedia.org/wiki/Oblique_Strategies) for today.


---
created: 2026-06-30T12:08:05.810Z
updated: 2026-06-30T12:08:05.810Z
---
> This is Prism, a proof of concept functional compiler I've been working on for the last three years, built around modeling effects with modern types inspired by the intellectual lineage of OCaml 5, Haskell and Koka. The big idea of the last five or six years of functional programming is that effects are real, effects are fine, and the interesting question is not how to avoid them but how to put them in the type system and then optimize them until they cost nothing.

- [Stephen Diehl](https://www.stephendiehl.com/posts/prism/)

This seems like basically a way to write Haskell-ish functional code, but avoid the monadic morass that can result.

It's a neat-looking language that lets you avoid types a lot more often than similar languages, apparently by including "effects" in the type system (warning: I'm way out over my skis talking about this topic)

I've stopped worrying that I'll ever need to use a functional programming language "for real" in my career, but this one seems different and neat.

https://github.com/sdiehl/prism

> The interpreter sits at the bottom of a proof chain whose top is Lean 4

Very cool! [[Lean]] is something I've played with, enough to get through a bit of [[The Natural Number Game]], but this is a whole other level I can't even comprehend.
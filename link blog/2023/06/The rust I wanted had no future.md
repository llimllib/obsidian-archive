---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
Graydon Hoare [writes a long piece](https://graydon2.dreamwidth.org/307291.html) about the features in [[rust]] he wishes had turned out differently, and lays out why he's glad/thinks everyone should be glad that he's actually not the BDFL of rust.

I think the post is interesting for a couple of reasons, even though I don't use rust:
- I really like his general, calm, attitude
- I like thinking about all the different parameters in the design space that _weren't_ chosen, even if I don't entirely understand rust it gives me a better sense for how large the design space of programming languages is. It's huge!
	- he wants types similar to [[zig]]'s comptime types (links [this piece](https://soasis.org/posts/a-mirror-for-rust-a-plan-for-generic-compile-time-introspection-in-rust/) which I haven't read)
	- wishes for a simple grammar and tail calls
- I appreciate his humility

> The point is to indicate _thematic divergence_. The priorities I had while working on the language are broadly not the revealed priorities of the community that's developed around the language in the years since, or even that were being-revealed in the years during. **I would have traded performance and expressivity away for simplicity** -- both end-user cognitive load and implementation simplicity in the compiler -- and by doing so I would have taken the language in a direction _broadly_ opposed to where a lot of people wanted it to go.  
  
> ...If I'd stayed in charge (or even asserted a more robust sense of "being in charge" when I was _nominally_ moreso) the result would have been, I think, fairly unpopular. The Rust I Wanted probably had no future, or at least not one anywhere near as good as The Rust We Got. The fact that there was _any_ path that achieved the level of success the language has seen so far is frankly miraculous. Don't jinx it by imagining I would have done any better!
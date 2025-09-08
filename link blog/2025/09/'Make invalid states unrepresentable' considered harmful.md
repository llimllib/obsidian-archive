---
created: 2025-09-08T15:11:29.080Z
updated: 2025-09-08T15:11:29.081Z
---
https://www.seangoedecke.com/invalid-states/

> One of the most controversial things I believe about good software design is that **your code should be more flexible than your domain model**. This is in direct opposition to a lot of popular design advice, which is all about binding your code to your domain model as tightly as possible.

via [lobste.rs](https://lobste.rs/s/itj50a/make_invalid_states_unrepresentable)

An interesting article for me, because I agree and disagree with lots of parts of it. Then I think that actually maybe it's underspecified and we'd agree with fuller context.

> The principle here is the same as with state machines: **at some point you will be forced to do something that violates your tidy constraints**, and if you’ve made those constraints truly immovable you’re buying yourself a lot of trouble.

I do agree with that! But "truly immovable" is doing some very heavy lifting, oftentimes you do really want some constraint to be "nearly immovable" or to intentionally have friction, lest you encourage it as a path.

I've heard "If you open your mind too far, your brain will fall out", and something similar happens with flexibility in programming systems. **If you make your system too flexible, it will fall apart** into a heaping mass of conditional statements that nobody can follow.

The way I tend to think about flexibility is related to the ["Imperative shell, functional core"](https://www.destroyallsoftware.com/screencasts/catalog/functional-core-imperative-shell) maxim; your program should have a flexible shell that accepts almost anything, but removes flexibility and passes inflexible domain objects into the core of the program.

If you leave the data store reasonably flexible (by avoiding foreign key constraints for example, as [discussed in the article](https://www.seangoedecke.com/invalid-states/#:~:text=are%20not%20absolute.-,foreign%20key%20constraints,-Another%20classic%20example), you can create dual paths for requests to the system: the main path for 95% of the requests goes through the normal, inflexible path where the domain assumptions hold, while the other 5% do something different.

What they do depends on the system - maybe there's an alternate path, maybe they get routed to a human - but you can handle the exceptional requests, exceptionally.

---

The lobste.rs comments also point to [Pure and Impure engineering](https://www.seangoedecke.com/pure-and-impure-engineering/), which is another thought-provoking article I'd like to write about in the future.

---

I also enjoy [this link](https://news.ycombinator.com/item?id=18190005) to a hacker news comment from `kentonv` defending some design decisions in protobufs, especially relating to the "all fields are optional" design.

I love the argument that the value of allowing intermediary systems to pass through messages they can't successfully parse is very high, and extremely underrated
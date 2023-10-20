https://www.scattered-thoughts.net/writing/how-safe-is-zig/

Very thorough and balanced article on the memory safety of zig, compared mainly to rust and C/C++

> In [materialize](https://github.com/MaterializeInc/materialize/) we wrote ~140kloc of rust in the first 14 months while growing the team from ~3 to ~20 people. It's a complex system with high demands on both throughput and latency. We reached that point with (IIRC) only 9 unsafe blocks, all of which were in a single module and existed to work around a performance bug in the equivalent safe api. Despite heavy generative testing and fuzzing, we only discovered one memory safety bug (in the unsafe module, naturally) which was easy to debug and fix.

> By comparison, in several much smaller and much simpler zig codebases where I am the only developer, I run into multiple memory safety bugs per week. This isn't a perfect comparison, because my throwaway research projects in zig are not written carefully (=> more bugs added) but are also not tested thoroughly (=> fewer bugs detected). But it does make me doubt my ability to ship secure zig programs without substantial additional mitigations.

> In at least one of those codebases, the memory safety bugs are outnumbered 20:1 by bounds-check panics. So I assume that if I wrote that same project in idiomatic c (ie without bounds checks) then I would encounter at least 20x as many memory safety bugs per week.

...

> In the long run, if rust (and other memory-safe languages) can be used everywhere but zig is only usable in certain niches, then network effects will give rust a huge advantage even in those niches. So I suspect zig's future, at least in my field, hinges on the successful development of cheap runtime mitigations.
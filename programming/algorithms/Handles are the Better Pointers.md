---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://floooh.github.io/2018/06/17/handles-vs-pointers.html

Describes the pattern of programs with subsystems that give out integer handles, which represent indexes into internal arrays, rather than allowing allocations all over the place.
- Improves cache locality
- Improves memory layout
- Provides a clear organziational pattern

Gives some good explanation of the rules to put in place if you adopt this pattern, and how to avoid dangling handles.

via responses to [this tweet](https://elk.pwm.social/vis.social/@adrian@discuss.systems/109990979632589853)

> Compiler people like to use arenas a lot: like, where you pack an expression tree into an array and use plain ol’ integer offsets instead of pointers to refer to nodes in the tree. The benefits are many: less allocation, smaller references, better locality, easier to think about lifetimes.

> But I’ve never seen this technique taught in a class. Does anybody know of basic resources that explain the idea? Maybe I should add it to my compilers curriculum, even though it’s not a compiler-specific idea at all?
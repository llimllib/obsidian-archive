---
created: 2024-07-13T13:03:01.930Z
updated: 2024-07-13T13:03:01.930Z
---
https://www.mattkeeter.com/blog/2024-07-12-interpreter/

> In modern times, everyone knows that writing assembly is a fool's errand: compilers are the result of literal engineer-centuries of work, and they know the processor much better than you do.

> And yet – one hears _rumors_.

> Written in [ancient tomes](https://jilp.org/vol5/v5paper12.pdf), muttered in [quiet watering holes](http://lua-users.org/lists/lua-l/2011-02/msg00742.html), scrawled on the walls of [bygone temples](https://www.reddit.com/r/programming/comments/badl2/luajit_2_beta_3_is_out_support_both_x32_x64/c0lrus0/), hinted at by [mysterious texts](https://llvm.org/docs/LangRef.html#calling-conventions); the rumors paint a specific picture:

> > Compilers are bad at generating code for interpreters, and it's possible to outperform them by writing your interpreter in assembly.

I've only quoted the start, because the whole thing is absolutely worth reading if you care about this sort of thing.

I have mostly no idea at all how to read [[assembly]], and I still found it enlightening!

The article also mentions [[luajit]] techniques, which I've previously linked in [[Building the fastest Lua interpreter... automatically]] and [[Building a baseline JIT for Lua automatically]]
https://www.pypy.org/posts/2024/03/fixing-bug-incremental-gc.html

Enjoyed this piece from CF Bolz-Tereick, who explains in detail how they tracked down a complicated bug in the [pypy](https://www.pypy.org/) interpreter that managed to survive for a full decade.

I had never heard of the [GDB python scripting API](https://sourceware.org/gdb/current/onlinedocs/gdb.html/Python-API.html) before, it's a neat-looking tool.

> The way the bug was introduced is really typical. A piece of code (the memcopy write barrier) was written under a set of assumptions. Then those assumptions changed later. Not all the code pieces that relied on these assumptions to be correct were updated. It's pretty hard to prevent this in all situations.

> I still think we could have done more to prevent the bug occurring. Writing a property-based test for the GC would have been a good idea given the complexity of the GC, and definitely something we did in other parts of our code at the time (just using the `random` module mostly, we started using [[hypothesis]] later).
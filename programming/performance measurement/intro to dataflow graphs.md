---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://fgiesen.wordpress.com/2018/03/05/a-whirlwind-introduction-to-dataflow-graphs/

> say we have some piece of C++ code that we’re trying to understand (and perhaps improve) the performance of. A good first step is to profile it, which will give us some hints _which_ parts are slow, but not necessarily _why_. On a fundamental level, any kind of profiling (or other measurement) is _descriptive_, not _predictive_: it can tell you how an existing system is behaving, but if you’re designing something that’s more than a few afternoons worth of work, you probably don’t have the time or resources to implement 5 or 6 completely different design alternatives, pick whichever one happens to work best, and throw the rest away. You should be able to make informed decisions up front from an algorithm sketch without having to actually write a fleshed-out implementation.

> if we want to go deeper than just squinting at C/C++ code and doing some hand-waving, we need to start looking at a somewhat lower abstraction level and define a machine model that is more sophisticated than “statements execute one by one”...
> Instead, what I’m going to do is use a simplified machine model that allows us to make quantitative predictions about the behavior of straightforward compute-bound loops, which is simple to describe but still gives us a lot of useful groundwork for more complex scenarios.
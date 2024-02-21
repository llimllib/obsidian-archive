> if you look at almost any significant open source project you will see hundreds, even thousands of dependencies in the fully realized import tree, dependencies that are never checked, updates that are never verified as safe. Essentially no one maintains their dependency tree as they should, because it is infeasible to do so. We have built a machine that cannot be fixed.

- [Rob Pike](https://phanpy.social/#/hachyderm.io/s/111960728489364881)

Somebody below that toot links to [this 2008 interview with Knuth](https://www.informit.com/articles/article.aspx?p=1193856). Some excerpts:

> the idea of immediate compilation and "unit tests" appeals to me only rarely, when I’m feeling my way in a totally unknown environment and need feedback about what works and what doesn’t. Otherwise, lots of time is wasted on activities that I simply never need to perform or even think about. Nothing needs to be "mocked up."

...

> Let me put it this way: During the past 50 years, I’ve written well over a thousand programs, many of which have substantial size. I can’t think of even _five_ of those programs that would have been enhanced noticeably by parallelism or multithreading. Surely, for example, multiple processors are no help to TeX.[

...

> literate programming is certainly the most important thing that came out of the TeX project. Not only has it enabled me to write and maintain programs faster and more reliably than ever before, and been one of my greatest sources of joy since the 1980s—it has actually been _indispensable_ at times. Some of my major programs, such as the MMIX meta-simulator, could not have been written with any other methodology that I’ve ever heard of. The complexity was simply too daunting for my limited brain to handle; without literate programming, the whole enterprise would have flopped miserably.

...

> I also must confess to a strong bias against the fashion for reusable code. To me, "re-editable code" is much, much better than an untouchable black box or toolkit. I could go on and on about this. If you’re totally convinced that reusable code is wonderful, I probably won’t be able to sway you anyway, but **you’ll never convince me that reusable code isn’t mostly a menace.**

(emphasis mine)
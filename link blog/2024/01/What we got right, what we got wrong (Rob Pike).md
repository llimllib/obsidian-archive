https://commandcenter.blogspot.com/2024/01/what-we-got-right-what-we-got-wrong.html

I'd meant to get to watching this, and finally made the time this morning.

<iframe width="560" height="315" src="https://www.youtube.com/embed/yE5Tpp2BSGw?si=daF1QcYFcsmFmsBx" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

- I like that he calls it "server software" rather than "system software". In my head, I think of Go as a domain language for writing server software, and frequently see arguments over somebody calling it appropriate for "system software".
---
> Go's version of concurrency was somewhat novel, at least in the line of languages that led to it, by making goroutines unflavored.  No coroutines, no tasks, no threads, no names, just goroutines. We invented the word "goroutine" because no existing term fit. And to this day I wish the Unix spell command would learn it.

> As an aside, because I am often asked about it, let me speak for a minute about async/await.  It saddens me a bit that the async/await model with its associated style is the way many languages have chosen to support concurrency, but it is definitely a huge improvement over pthreads.

---

> In short, although I wouldn't change a thing about how interfaces worked, they colored our thinking in ways it took more than a decade to correct. Ian Taylor pushed us, from early on, to face this problem, but it was quite hard to do given the presence of interfaces as the bedrock of Go programming.

> Critics often complained we should just do generics, because they are "easy", and perhaps they can be in some languages, but the existence of interfaces meant that any new form of polymorphism had to take them into account. Finding a way forward that worked well with the rest of the language required multiple attempts, several aborted implementations, and many hours, days, and weeks of discussion. Eventually we roped in some type theorists to help out, led by Phil Wadler.  And even today, with a solid generic model in the language, there are still lingering problems to do with the presence of interfaces as method sets.

---

> The early compiler worked. It bootstrapped the language well. But it was a bit of an odd duck, in effect a Plan 9-style compiler using old ideas in compiler writing, rather than new ones such as static single assignment.  The generated code was mediocre, and the internals were not pretty.  But it was pragmatic and efficient, and the compiler code itself was modest in size and familiar to us, which made it easy to make changes quickly as we tried new ideas. 

> ...Doing it our way, however unorthodox, helped us move fast. Some people were offended by this choice, but it was the right one for us at the time.

I love the idea of valuing flexibility and comfort more highly than fully modern features.

---

> The key missing piece was examples of even the simplest functions. We thought that all you needed to do was say what something did; it took us too long to accept that showing how to use it was even more valuable.

> That lesson was learned, though. There are plenty of examples in the documentation now, mostly provided by open source contributors. And one thing we did very early was make them executable on the web.

[[Cookbook documentation]]!

---

> Perhaps the most interesting consequence of these matters is that Go code looks and works the same regardless of who's writing it, is largely free of factions using different subsets of the language, and is guaranteed to continue to compile and run as time goes on. That may be a first for a major programming language.


> We definitely got that right.

---
paraphrasing from the Q&A:

> One thing I wish we'd done was to use arbitrary precision integers from the start... that's the thing I would most like to see happen

amen!
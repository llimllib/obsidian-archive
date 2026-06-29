---
created: 2026-06-23T13:21:38.669Z
updated: 2026-06-23T13:21:38.669Z
---
> Present-day models tend to produce code that is too defensive, too complex, too local in its reasoning. They avoid strong invariants. They add fallbacks instead of making bad states impossible. They duplicate code, invent bad abstractions, and paper over unclear design with more machinery. Worse though: I so far see very little progress of this improving. If anything, on that front it feels to me that we might even be making steps in the wrong direction. At least for my taste, present-day hands-off harnesses like Claude Code with ultracode produce worse code than what we were producing last autumn. That’s because Claude Code, with Fable for instance will be working uninterrupted on a problem for thirty minutes or more, when previously the process would have been much more human in the loop.

> Furthermore it’s well understood that models tend to observe some local failure and add a local defense. [Karpathy mentioned](https://x.com/karpathy/status/1976082963382272334) how they are “mortally terrified of exceptions”. In systems with important invariants, especially persisted data formats or core infrastructure, the right fix is not “handle every malformed case.” The right fix is to make the malformed case unrepresentable or impossible to write in the first place. Yet even with a lot of manual steering, that type of code does not come out of LLMs naturally, and even if the code comes out naturally like that, they will still attempt to handle now impossible errors.

- [Armin Ronacher](https://lucumr.pocoo.org/2026/6/23/the-coming-loop/)

This has been my experience as well. I prefer using [[pi]] in large part because it doesn't hide those loops from you, so I at least more often notice when the machine is doing something stupid, or doing something local that ought to be global.

The whole piece is well worth reading, as you might guess from my long pull quote.

> The scariest part to me is that we become dependent on these new machines in new ways. Software has always depended on tools. I remember the time when I had to pay for compilers. These new tools are a flashback to times where creating software came with real costs. But now it’s no longer a one-time payment, it’s a constant dependency. Not just a dependency on a filled wallet, but also a cognitive dependency.

This is also my #1 fear
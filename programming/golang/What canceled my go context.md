---
created: 2026-04-06T12:59:38.799Z
updated: 2026-06-10T19:41:03.640Z
---
https://rednafi.com/go/context-cancellation-cause/

Excellent article walking through one of the finer points of context usage: figuring out what cancelled your context.

Gives examples of how to make sure you can always figure it out.

---

brandur starts with the same `context.WithTimeoutCause`, but gives a different recipe, describing a function `timeoututil.AttributedTimeout` that takes a closure and handles context deadlines from within that closure
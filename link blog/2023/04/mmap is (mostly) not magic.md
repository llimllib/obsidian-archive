---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://twitter.com/jeremyphoward/status/1642726595436883969

Good thread discussing yesterday's mistaken belief by many that the 30b param LLama LLM could be fit in under 6gb of ram by mmap'ing it. Goes through the network architecture to explain why most of the map has to live in memory, no matter what you do.

> The way mmap handles memory makes it a bit tricky for the OS to report on a per-process level how that memory is being used. So it generally will just show it as "cache" use. That's why (AFAICT) there was some initial misunderstanding regarding the memory savings

> ...One interesting point though (mentioned in the GH issue) is that you can now have multiple processes all using the same model, and they'll share the memory -- pretty cool!
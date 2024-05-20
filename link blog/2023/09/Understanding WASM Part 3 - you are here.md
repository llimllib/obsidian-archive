---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://www.neversaw.us/drafts/understanding-wasm-pt-3/

A followup to the superb [[Understanding WASM]] part 2. Long and worth your time if you're at all interested in this stuff.

Random notes follow:

Starts with a walk through the history of Virtualization; I love this diagram:

![[virtual-memory-paging.png]]

> Illustration from ["Segmentation and the Design of Multiprogrammed Systems"](https://dl.acm.org/doi/pdf/10.1145/321296.321310), Jack B. Dennis, 1965. "N" represents the process address namespace, "M" the physical namespace. Note how the contiguous "N" namespace maps to a discontiguous namespace in "M".

- Links to [[Putting the "you" in CPU]] and [this interesting-looking series on writing an OS in Rust](https://os.phil-opp.com/paging-introduction/) that I had not seen before.
- Includes the clearest explanation of Xen virtualization I have read yet, and I was around when it was released.

> `fork` and `exec` form the bedrock of the POSIX process model. Their descendants, `clone` and `unshare`, form the basis for working with Linux cgroups and namespaces. In short, it is hard to support `fork` without also taking the traditional process model on board. And WebAssembly [may not want to do that](https://www.microsoft.com/en-us/research/uploads/prod/2019/04/fork-hotos19.pdf).

----

> Instead of one monolithic wall of functions representing all system services, the WASM Component Model proposes a system of smaller fences placed between every module. Each interface only specifies the functionality it needs, and may be fulfilled by any other module — or the host. Instead of exposing entire namespaces of functionality, like `mnt`, `uts`, or `net`, the interface can be described in a fine-grained way: "module A requires a function for reading input data."

> This allows sockets to be represented as higher level objects whose full capabilities aren't transferred between linked modules, as opposed to an integer descriptor tracked by the host. (See Dan Gohman's excellent ["No Ghosts!"](https://blog.sunfishcode.online/no-ghosts/) for more on this.)

----

> It's the human side of computing: it is better to be in a room full of people gathered around the warmth of an imperfectly useful interface than it is to be out, alone in the cold, with a perfect interface.

----

Includes a really thorough and excellent list of resources at the end, which I will undoubtedly fail to read most of and feel slightly guilty about it
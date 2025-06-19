---
created: 2025-06-19T14:38:03.196Z
updated: 2025-06-19T14:38:03.196Z
---
https://rjp.io/blog/2025-06-17-unreasonable-effectiveness-of-fuzzing

> LLMs open up the door to performing radical updates that we'd never really consider in the past. We can port our libraries from one language to another. We can change our APIs to fix issues, and give downstream users an LLM prompt to migrate over to the new version automatically, instead of rewriting their code themselves. We can make massive internal refactorings. These are types of tasks that in the past, _rightly_, a senior engineer would reject in a project until its the last possibly option. Breaking customers almost never pays off, and its hard to justify refactoring on a "maintenance mode" project.

> But if its more about finding the right prompt and letting an LLM do the work, maybe that changes our decision process.

---

> What happens if we take a very specific and important type of refactoring: moving from an unsafe language like C to a safe language like Rust? "I did something with memory I shouldn't have" are still in the [top 3 for CVEs](https://www.cvedetails.com/vulnerabilities-by-types.php)No longer #1, not because the number of memory CVEs is going down, but because XSS vulnerabilities have grown so quickly 🤦. . This is exactly the type of thing we might _like_ to do, but hard to justify. Can we make porting more of a prompt engineering problem instead of a coding one? Let's find out...

---

> And in the end... it worked? The result is a [Rust implementation of Zopfli](https://github.com/rjpower/portkit/tree/main/zopfli-port) that gives_identical_ results on every input I've tried to the C version. This is different from the Syzygy results, where they ended up with a program that compresses correctly, but not identically to the C version. Because we locked the Rust and C versions to use the same API at each step, the resulting program isn't very "rusty", but its a complete translation.

My main takeaway from this experiment is how much skill is involved in getting LLMs to make large changes at the moment; their chat interface is far from ideal and the author had to go through several experimental methods and eventually write their own small agent framework to get it to work.

But also, that some large refactors that would not have been feasible before are definitely feasible with LLMs, and that space is an exciting one
https://www.microsoft.com/en-us/research/uploads/prod/2018/03/build-systems.pdf

Andrey Mokhov, Neil Mitchell, and Simon Peyton Jones published this already-classic paper in 2018.

It breaks down build systems (including ${ Excel}$!) in several dimensions to look at exactly what they do, and think about where the gaps are that productive build systems might fit in.

I don't follow much of the haskell code, but it's still a useful read.

> ${ Excel}$ is a build system in disguise. Consider the following simple spreadsheet:

```
A1: 10
A2: 20
B1: A1 + A2
```

> There are two input cells A1 and A2, and a single task that computes the sum of their values,
producing the result in cell B1. If either of the inputs change, $Excel$ will recompute the result.

> Unlike $Make$, ${ Excel}$ does not need to know all task dependencies upfront. Indeed, some dependencies may change dynamically according to computation results.

> To support dynamic dependencies, ${ Excel}$’s calc engine is significantly different from $Make$. $Excel$ arranges the cells into a linear sequence, called the calc chain. During the build, $Excel$ processes cells in the calc-chain sequence, but if computing a cell C requires the value of a cell D that has not yet been computed, $Excel$ _aborts_ computation of C, moves D before C in the calc chain, and resumes the build starting with D. When a build is complete, the resulting calc chain respects all the dynamic dependencies of the spreadsheet. When an input value (or formula) is changed, $Excel$ uses the final calc chain from the _previous_ build as its starting point so that, in the common case where changing an input value does not change dependencies, there are no aborts.

---

They define these axes on which build systems differ:

- Scheduling
	- Topological: pre-compute the task list to build
	- Restarting: just start building, and if your task requires some $dep$, stop what you're doing, build $dep$, and restart when it's done
	- Suspending: just start building, and if your task requires some $dep$, pause what you're doing while you build $dep$, then carry on
- Rebuilding
	- A dirty bit: there is some marker on an object of whether it needs rebuilt; in make it's the file's `mtime` compared to its build output
	- Verifying traces: record a hash of what you built last time, and only build if the hash is different
	- Constructive traces: record the actual built value instead of a hash

![[Pasted image 20240319160907.png]]

a classic paper I hadn't read probably since it came out, it was nice to remember it!

I got to it this time from a link on [this article](https://yzena.com/2024/03/build-system-schism-the-curse-of-meta-build-systems/), "Build system schism: the curse of meta build systems"
---
updated: '2024-02-20T15:00:51Z'
created: '2024-02-20T15:00:51Z'
---
https://danluu.com/simple-architectures/

> for most kinds of applications, even at top-100 site levels of traffic, computers are fast enough that high-traffic apps can be served with simple architectures, which can generally be created more cheaply and easily than complex architectures.

It's interesting that he argues that a Kubernetes-backed app running graphql is a "simple architecture"; I'm not disagreeing but it reinforces to me that what "simple" means is extremely context-dependent.

"Simple" often means "things that are reasonably common knowledge on our team".

A corollary of that is that, by education and practice, you can _change_ what it means for something to be simple! Simple is what you do, and what you do is what's simple **as long as it's well understood**.

If it's not well understood, by which I mean that deep understanding of the system is either not present at all, or not well-distributed among your team, then that's what complexity is.
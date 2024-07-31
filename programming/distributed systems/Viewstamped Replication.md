---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://pmg.csail.mit.edu/papers/vr-revisited.pdf

> This paper presents an updated version of Viewstamped Replication, a replication technique that handles failures in which nodes crash. It describes how client requests are handled, how the group reorganizes when a replica fails, and how a failed replica is able to rejoin the group. The paper also describes a number of important optimizations and presents a protocol for handling reconfigurations that can change both the group membership and the number of failures the group is able to handle.

The replication protocol implemented by TigerBeetle, via [this article](https://matklad.github.io/2023/03/26/zig-and-rust.html) about the author's experience with rust and [[zig]], respectively.

They point to [this architecture doc](https://github.com/tigerbeetledb/tigerbeetle/blob/fe09404d465df46b2bdfc017633eff37b4ab2343/docs/DESIGN.md) for TigerBeetle, which includes reasoning for the choice of algorithm and other choices they have made.
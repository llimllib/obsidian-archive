https://github.com/richardartoul/tsdb-layer

Demonstration time series database layer for [[FoundationDB]]

> I built DiamondDB purely as a PoC to measure performance of different architectures for storing time series data in FoundationDB. It is in no way production ready. In fact, the code is littered with TODOs, cut corners, and missing features. The only thing DiamondDB is useful for in its current form is demonstrating how a performant time series database **could** be built on-top of FDB

> But why does FDB make for such a good primitive? To answer that question, we first need to understand the data model of FoundationDB. FoundationDB is a distributed system that provides the following semantics:

1.  Key/Value storage where keys and values can be arbitrary byte arrays.
2.  Keys are "sorted" lexicographically such that reading and truncating large sorted ranges is efficient.
3.  Automatic detection and redistribution of hot keys (this one is particularly unique and I’m not aware of many other systems that handle this gracefully).
4.  Completely ACID transactions at the highest level of isolation `strict serializability` across arbitrary key/value pairs.

> FoundationDB is fast, reliable, easy to use, and a lot of fun to program against. Next time you need to build a distributed system consider if FDB could make your job a little bit easier. You might be surprised by just how far you can push it with the right design.
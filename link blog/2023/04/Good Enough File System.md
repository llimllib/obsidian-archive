https://orib.dev/gefs.html

> Gefs is a new file system built for Plan 9. It aims to be a crash-safe, corruption-detecting, simple, and fast snapshotting file system, in that order. Gefs achieves these goals by building a traditional 9p file system interface on top of a forest of copy-on-write Bε trees. It doesn't try to be optimal on all axes, but good enough for daily use.

> Gefs asks the question: What would have happened if we stopped at a simple, easy to understand copy on write file system, and went "that's good enough"?

> How far might we get without making significant sacrifices?

...

> Finally, the entire file system is based around a relatively novel data structure. This data structure is known as a Bε tree [1]. It's a write optimized variant of a B+ tree, which plays particularly nicely with copy on write semantics. This allows gefs to greatly reduce write amplification seen with traditional copy on write B-trees.


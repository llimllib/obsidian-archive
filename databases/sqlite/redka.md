https://github.com/nalgeon/redka

> Redka aims to reimplement the good parts of Redis with SQLite, while remaining compatible with Redis API.

A neat project! It's a wrapper around [[sqlite]] that supports the [[redis]] protocol.

[Here's the implementation of the `set` command](https://github.com/nalgeon/redka/blob/9b2dec3771b365024092c9f637c1676d521e1571/internal/command/set.go), for example. It ends up pretty abstracted from the database.

found via [news.yc](https://news.ycombinator.com/item?id=40030746)

Performance is, unsurprisingly, much worse than redis. Reads are approximately 2x slower on a simple benchmark run, writes between 4.5x - 6x slower. It also has very different characteristics, being an ACID-compliant wrapper rather that wants to be safe on disk rather than a highly performant in-memory store that will write to disk in any of several potentially unsafe ways.

I'm not quite sure if I would ever want to use it! But it's neat.
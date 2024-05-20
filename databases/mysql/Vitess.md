---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
> Vitess is a meta-layer on top of MySQL shards that asks, per table, which key to shard on. It then uses that information to maintain some distributed indexes of its own, and to plan the occasional scatter/gather query appropriately.

used by slack, from this excellent comment by a former slack chief architect: https://news.ycombinator.com/item?id=27199360

praised by tmcw on twitter

seems like it could be useful for any client-facing big DB problems... not sure how good the deployment story is

https://vitess.io/

> A database clustering system for horizontal scaling of MySQL

uses protobuf: https://vitess.io/blog/2021-06-03-a-new-protobuf-generator-for-go/

https://slack.engineering/scaling-datastores-at-slack-with-vitess/

Not exactly sure how it's different from/similar to [[Citus]] having never used either

[[MySQL]]

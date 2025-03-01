---
created: 2025-03-01T14:06:46.304Z
updated: 2025-03-01T14:06:46.304Z
---
Neat stat I saw from [Lev Akabas](https://bsky.app/profile/levakabas.bsky.social/post/3ljasknpp5s26v) in use for shooting efficiency charts, opposed to usage %:

FGA + 0.5 * (FTA - And 1 chances)

The challenge is I don't know where he gets "And 1 chances", which is necessary to avoid double-counting those FGAs; probably there aren't enough that it would matter substantively, and you could just use `fga + .5 * fta` well enough?
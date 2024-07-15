---
created: 2024-07-14T13:35:42.520Z
updated: 2024-07-14T13:35:42.520Z
---
https://github.com/carderne/upid

Very similar to [[typeid]], UPID is a UUID spec that embeds four prefix characters _inside_ a 128-bit UUID string, instead of prefixing a full UUID like typeid does.

The cost is fewer bits for the time (48 -> 40 bits) and randomness (80 -> 64)
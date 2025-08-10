---
created: 2025-08-10T14:27:53.177Z
updated: 2025-08-10T14:27:53.177Z
---
https://blog.hyperknot.com/p/openfreemap-survived-100000-requests

Blog from the creator of [[openfreemap]] on how their site survived a DDos with the help of cloudflare.

I'm glad to see that they're still going with the project, and there are some interesting thoughts on high-performance tile serving in the [news.yc comments](https://news.ycombinator.com/item?id=44846318)

- The author is using nginx and an option for caching open file handles, and there's discussion on whether that's actually valuable on a fast NVMe drive
- There's an interesting question of how to handle empty files:
	- > To optimize for ocean areas, tiles that don’t exist on disk should be served as a `200 OK` with an empty body. These are then rendered as empty space on the map.
- The author posted in the [nginx forum](https://community.nginx.org/t/too-many-open-files-at-1000-req-sec/5796?u=hyperknot) with some detailed perf questions; the question is worth reading but unfortunately does not have any replies yet
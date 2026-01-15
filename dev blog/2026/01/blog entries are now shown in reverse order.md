---
created: 2026-01-01T15:17:51.723Z
updated: 2026-01-01T15:17:51.723Z
---
The "blog"s on this website are just directories whose folders happen to contain folders named after years and months. Until this morning, they were displayed in alphabetical order just like every other folder - which is in chronological order instead of reverse chronological as blogs are normally displayed.

My blog is now up to date with 1999 web practice and shows blogs in reverse chronological order!

- The change is [here](https://github.com/llimllib/obsidian_notes/commit/51c7b43441a1498356a72ecf5c6cb31f83609f64)

I use jinja for templating and it drives me kind of crazy because it's kind of similar to python, but not completely, and I don't use it often enough to remember how it works. To make this change, I used a typical pattern for me these days:

- express the change you want to see
	- In this case, I did `reverse(tree.children)`, which doesn't work in jinja
- ask the LLM how to fix it
	- the LLM reported that I should instead use the `reverse` filter, which worked perfectly
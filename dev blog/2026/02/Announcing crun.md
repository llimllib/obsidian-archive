---
created: 2026-02-12T01:03:33.541Z
updated: 2026-02-12T01:03:33.541Z
---
I've long liked [[concurrently]], a node program that runs multiple programs concurrently, interleaves their output, and adds prefixes telling you which program wrote the output.

I use it for running web sites in development, where for example you might want to run your task engine, a web server, and a development node server at the same time.

The annoying thing about it has always been that it's a node program - no stress if you're already in the node ecosystem but for other programs it can be annoying.

So, I created [crun](https://github.com/llimllib/crun), a port of `concurrently` to rust. Currently it stands at only 1.5 megabytes, and you can install it with cargo or homebrew.

If you've used `concurrently` or have wanted to, give it a shot! File an issue if it doesn't work for you, or you have ideas for improvement.

![[Pasted image 20260211203014.png]]
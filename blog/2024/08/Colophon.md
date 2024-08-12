---
created: 2024-08-12T20:54:18.364Z
updated: 2024-08-12T20:54:18.364Z
---
To add to this blog, I type out a note in Obsidian; I use Obsidian with very few plugins.

![[typenote.mp4]]

When it's reasonably done, I back it up with the [obsidian git](https://github.com/Vinzent03/obsidian-git) plugin by clicking the "backup" button

![[Pasted image 20240812170051.png]]

That backs it up to a private github repository.

That repository has a [github action](https://gist.github.com/llimllib/19bbe748d13da49233d501da04e63fb8) that runs [run.py](https://github.com/llimllib/obsidian_notes/blob/d745eae34ac9f261baa7dbba093240b73a71945c/run.py) from my [obsidian_notes repository](https://github.com/llimllib/obsidian_notes).

That script converts the big pile of Obsidian-flavored markdown into a big pile of HTML.

The github action uploads that big pile of HTML to a [Digital Ocean space](https://www.digitalocean.com/products/spaces) using [[s3cmd]]. (I [don't recommend](https://hachyderm.io/@llimllib/112759682584953702) Digital Ocean spaces, but that's what I use for now)

To serve `notes.billmill.org`, I have [[caddy]] installed on my web server, proxying requests to `cdn.billmill.org`, which is a `CNAME` to the digital ocean space.

That's it! Feel free to ask me questions on mastodon.


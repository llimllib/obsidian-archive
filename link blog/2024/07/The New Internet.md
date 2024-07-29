---
created: 2024-07-29T19:21:09.765Z
updated: 2024-07-29T19:21:09.765Z
---
> In modern computing, we tolerate long builds, and then docker builds, and uploading to container stores, and multi-minute deploy times before the program runs, and even longer times before the log output gets uploaded to somewhere you can see it, all because we’ve been tricked into this idea that everything has to scale. People get excited about deploying to the latest upstart container hosting service because it only takes tens of seconds to roll out, instead of minutes. But on my slow computer in the 1990s, I could run a perl or python program that started in milliseconds and served way more than 0.2 requests per second, and printed logs to stderr right away so I could edit-run-debug over and over again, multiple times per minute...

> As an industry, we’ve spent all our time making the hard things possible, and none of our time making the easy things easy.

- [Avery Pennarun](https://tailscale.com/blog/new-internet)

He then goes on to imagine a tailscale-centric internet, when laying out his vision for what tailscale can bring.

I love tailscale! But I'll be honest that I don't understand how it could be a fundamental part of the internet when I can only share something I host with it with two people for free.

(I know there's [an open source control server](https://github.com/juanfont/headscale), but I have trouble seeing it in regular use by Actual Humans)
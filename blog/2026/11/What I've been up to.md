---
created: 2026-11-15T21:19:21.479Z
updated: 2026-11-15T21:19:21.479Z
---
Most of my spare-time effort has been going into my NBA projects:
- https://billmill.org/nba/ is my site with charts, stats, and tables
- It's powered by https://github.com/llimllib/nba_data , my github project to collect accurate current and historical NBA stats in a coherent database
- https://github.com/llimllib/yarapm/ is my own RAPM rating, something I've wanted to build for a long time but now I finally have the means to do so

Something cool and also scary about having coding agents is the ability to reach beyond your normal grasp, and yarapm is a good example of that. It's very cool that I'm able to build something that would have previously been beyond my ability to understand in my spare time, but it's also frightening because maybe I've gotten everything horribly wrong.

I can say the words "it's a ridge regression", and even kind of understand what it means, but coding up a RAPM calculator for myself would always have been just a bit beyond what I could reach, and if I'd gotten it done it would have been difficult to change because it's far from what I've built previously and would take a lot of work to understand.

With agents, I can say "here's the data, build me a RAPM", and it just does it. It's not actually even very much code! But it lets me think at the conceptual level, coming up with a [series of experiments](https://github.com/llimllib/yarapm/issues?q=sort%3Aupdated-desc+is%3Aissue+state%3Aopen+label%3Aexperiment) I want to run to see if they improve the model's output. I can even have it [write me a book](https://llimllib.github.io/yarapm/) about how it works so that I can know more about what I mean when I say "ridge regression".

### brightlantern

One other thing I've hacked on is [brightlantern](https://github.com/llimllib/brightlantern), which is a search engine for agent sessions that embeds a small vector search model in sqlite (using [sqlite-vec](https://github.com/asg017/sqlite-vec)) so that you don't have to search for the exact term to find a result.

It's distributed as a signed mac app on homebrew, so `brew tap llimllib/tap/brightlantern` will install it if you're interested in trying it out.
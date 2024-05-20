---
updated: '2024-04-26T14:54:59Z'
created: '2024-02-01T20:41:33Z'
---
> For better or worse, my experience as a GitHub cofounder and author of several Git books (Pro Git, etc) is that the Git commit message is a unique vector for code documentation that is highly sub-optimal.

> The main issue is that most of the tooling (in Git or GitHub or whatever) generally only shows the first line. So in the case of this commit example would be the very simple message of a generic "US-ASCII error" problem. Everything they talk about in this article is what is great about the _rest_ of the commit message, which, given modern tools, is _almost never_ seen by anyone.

> The main problem is that Git was built so that the commit message is the _email body_, meant to be read by everyone in the project. But for better or worse, that is not generally the role of this text today. Almost nobody ever sees it. Unless it's discussed in a bunch of patch series over a mailing list, nobody reads anything other than the first 50 chars of the headline. It's actively difficult to do, by nearly every tool built around the Git ecosystem.

> Even if you're _very good_ at Git, finding the correct invocation of "git blame" (is it "-w -C -C -C"? Or just _two_ dash C's?) to even find the right messages that are relevant to the code blocks you care about is not widely known and even if you find them, still only show the first line. Then you need to "git show" the identified commit SHA to get this long form message. There is just no good way to find this information, even if it's well written.

> This is one of my biggest complaints with Git (or, indeed, any VCS before it), and I think why people just don't care much about good commit messages. It's just not easy to get this data back once it's written.

> If you want an example of this, search through the Git project's history. Run a blame on any file. It's _so hard_ to figure out a story of any function implementation in any file, but the commit messages are _pristine_. Paragraphs and paragraphs of high quality explanation for almost every single commit. Look at any single commit that Jeff King has done for the last decade. Hundreds of hours of amazing documentation from a true genius that almost nobody will ever appreciate. It's horrifying.

> I don't know exactly what the answer is, but the sad truth of Git is that writing amazing documentation via commit message, for most communities, is almost entirely a waste of time. It's just too difficult to find them.

- Scott Chacon [on news.yc](https://news.ycombinator.com/item?id=39218538)

I like writing git commit messages similar to the one discussed in the [article which prompted that comment](https://news.ycombinator.com/item?id=39217149), but I also recognize the truth of what Scott is saying - approximately nobody ever reads them.

---

An idea following a [good discussion on mastodon](https://merveilles.town/@akkartik/111859196193506562):

A site where you enter a github repository's name, it does a bare checkout of the repo, then presents it with a blog-like interface, with an RSS feed and a search index

---

[further good discussion on mastodon](https://hachyderm.io/@sanityinc/112326951936274631); [here's. my response](https://hachyderm.io/@llimllib/112337781451381689) about how we currently do PR review at my employer, which I'm currently pretty happy with.
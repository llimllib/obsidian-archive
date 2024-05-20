---
updated: '2023-11-06T16:15:37Z'
created: '2023-11-06T16:15:37Z'
---
https://aeracode.org/2023/11/06/life-critical-side-projects/

Two interesting bits to me:

- Writing a social media app is frightening:

> several times during its development so far I've accidentally written bugs that would let you view private posts, force posts into people's timelines, or even post as other people. None of these are life-critical in the strict sense, but I get this unending feeling that I'm writing software that, if it ever got popular and something I screwed up ruined someone's life in even a small way, would absolutely destroy me.

> That's not something I enjoy, and in recent months I've struggled to find the energy to work on Takahē due to this feeling 

- On activitypub:

> Of course, while some of this is down to what it takes to work on social media software, the other part of it is that the Fediverse, with Mastodon-flavoured ActivityPub at its core, is not an easy place to just turn up and write a server in.

> While I have a lot of praise for it being an open standard people are actually using, it's an incredibly complex standard that, even after developing against it for over a year, I still don't fully understand - partially because there is no actual single standard that everyone adheres to, and there's plenty of weird behaviour and extensions.

> People keep asking me if they can just "plug in ActivityPub to their project" and... no, you can't. Being an ActivityPub server means handling so much in terms of state, subscriptions, fanout, and more, that you're better off just using an API to an existing server and posting there. My hat is off to the folks who actually made every single WordPress able to be a server.

I really dig Andrew's work on [takahe](https://github.com/jointakahe/takahe) and I hope he's successful in finding someone(s) to work on it, and wish him luck finding his next project.
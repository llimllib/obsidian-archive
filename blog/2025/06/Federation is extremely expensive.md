---
created: 2025-06-19T14:59:05.557Z
updated: 2025-06-19T16:04:16.190Z
---
There is a certain feeling among the developers of messaging software that if you want to create something worthwhile, you need to create a federated system.

This is how you get [ActivityPub](https://en.wikipedia.org/wiki/ActivityPub), [atproto](https://atproto.blue/en/latest/readme.html), [matrix](https://matrix.org/docs/chat_basics/matrix-for-im/), [xmpp](https://xmpp.org), [nostr](https://nostr.com), and on and on and on. A series of protocols that aim to recreate the successes of email and IRC.
### The successes are overblown

Email and IRC have huge problems, many of which are caused by their own decentralization.

Both protocols suffer from the extreme difficulty of upgrades - it's nearly impossible to organize a whole herd of people running servers to upgrade at the same time. The effect is that once a decentralized protocol has stabilized, it is extremely resistant to upgrades.

Both protocols suffer from the challenge of preventing spam. It has proven so difficult for email that is has de facto centralized around Google Mail and a few other major providers.

Email's design is extremely substandard by modern standards, but despite the quasi-centralization of providers, we have no hope of changing it because there are still too many providers and consumers to make modernization possible. This leaves us with the worst of both worlds, a sub-standard protocol with a mostly-centralized structure.
### Moderation is ~impossible

A key lesson of the modern internet is that a well moderated service is essential to providing a decent experience for users who are not trolls.

If your service is truly decentralized, consistent moderation is impossible by design.

Taking on federation means taking on the Herculean task of coordinating decentralized moderation. I don't think it's _impossible_ to do an OK job of it, but it's a huge task and an extreme social challenge.

### Ownership is important

I think a lot of the desire for federated systems comes down to a desire for **ownership**; the ability of a person or a group of people to own some piece of the system. It feels like in a decentralized system, even if you don't, you _could_ own a piece of it. You could stand up an email server, or a mastodon server, and do things your own way if you had to.

This is an excellent impulse, and we should nurture it!

But federation is not the only way to achieve ownership. We can make open software that allows people to own their own computation in meaningful ways a lot faster by **skipping federation** and focusing instead on building software that delivers a stronger user interface and user experience while providing data ownership.

I want to see is a world in which we can deliver more open software to develop communities more rapidly, and I think we might get there faster if we accept that the cost of federation is so high that we ought to consider avoiding it.

### postscript

This post follows a conversation I had on a private Slack. Part of the reason why I think that conversation happened on Slack instead of on an open chat system is that we have spent so much effort building federated systems that we've failed to deliver working open software to replace it.
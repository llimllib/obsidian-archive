---
created: 2024-10-21T12:42:46.225Z
updated: 2024-10-21T12:42:46.225Z
---
https://www.potaroo.net/ispcol/2024-10/ipv6-transition.html

> The data shows that the level of IPv6 use in the US has remained constant since mid-2019. Why is there no further momentum to continue with the transition to IPv6 in this part of the Internet? I would offer the explanation that the root cause is a fundamental change in the architecture of the Internet.

> The major change to the Internet’s architecture is a shift away from a strict address-based architecture. Clients no longer need the use of a persistent unique public IP address in order to communicate with servers and services. And servers no longer need to use a persistent unique public IP address to provide clients with access to the service or content. Address scarcity takes on an entirely different dimension when unique public addresses are not required to number every client and every distinct service...

> We may not route “names” in today’s Internet, but it is certainly operating in a way that is largely isomorphic to such a named data network.

And the conclusion:

> At this point it’s useful to ask: What “defines” the Internet? Is the classic response, namely: “A common shared transmission fabric, a common suite of protocols and a common protocol address pool.” still relevant these days? Or is today’s network more like: “A disparate collection of services that share common referential mechanisms using a common name space?”

> When we think about what’s important to the Internet these days is the choice of endpoint protocol addressing really important? Is universal unique end-point addressing a 1980’s concept whose time has come and gone? If network transactions are localised, then what is the residual role of unique global end point addressing for clients or services? And if we cannot find a role for unique end point addressing, then why should we bother? Who decides when to drop this concept? Is this a market function, so that a network that uses local addressing can operate from an even lower cost base gains a competitive market edge? Or are carriage services so cheap already that the relative benefit in discarding the last vestiges of unique global addresses so small that it’s just not worth bothering about?

- [Geoff Huston](https://www.potaroo.net/ispcol/2024-10/ipv6-transition.html)

Made me think of [my favorite piece](https://apenwarr.ca/log/20200708) on IPv6, by Avery Pennarun

> These (mostly) same people, when they started to realize the monster they had created, got worried. They realized that 32-bit addresses, which they had originally thought would easily last for the lifetime of their little internet, were not even enough for one address per person in the world. They found out, not really to anyone's surprise, that Postel's Law, unyielding as it may be, is absolutely a maintenance nightmare. They thought they'd better hurry up and fix it all, before this very popular Internet they had created, which had become a valuable, global, essential service, suddenly came crashing down and it would all be their fault...

> IPv6 was created in a new environment of fear, scalability concerns, and [Second System Effect](https://en.wikipedia.org/wiki/Second-system_effect). As we covered last time, its goal was to replace The Internet with a New Internet — one that wouldn't make all the same mistakes. It would have fewer hacks. And we'd upgrade to it incrementally over a few years, just as we did when upgrading to newer versions of IP and TCP back in the old days.
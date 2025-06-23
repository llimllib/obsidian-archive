---
created: 2025-06-23T17:41:31.110Z
updated: 2025-06-23T17:41:31.110Z
---
https://ergo.chat/
- [admin manual](https://github.com/ergochat/ergo/blob/stable/docs/MANUAL.md)
- [user guide](https://github.com/ergochat/ergo/blob/stable/docs/USERGUIDE.md)

> Ergo (formerly known as Oragono) is a modern IRCd (IRC server software) written in Go.

> Our core design principles are:

> - Being simple to set up and use.
> - Combining the features of an ircd, a services framework, and a bouncer (integrated account management, history storage, and bouncer functionality).
> - Bleeding-edge [IRCv3 support](https://ircv3.net/software/servers.html) suitable for use as an IRCv3 reference implementation.
> - High customizability via a rehashable (i.e., reloadable at runtime) YAML config.

I have a very poor opinion of IRC in general, but want to have an opinion of it that paints it in the best possible light. This seems like the most modern IRC server available.

Ergo provides chat history, which is table stakes IMO for a modern chat server, and paired with something like [kiwi IRC client](https://github.com/kiwiirc/kiwiirc) might provide a reasonable, modern, small, chat server of the kind I'm interested in.

Unfortunately (as far as I can tell) they only provide the web client for their test chat server and not for their `irc.ergo.net`; my attempts to connect to their server were not successful.

So I went to [irccloud.com](https://www.irccloud.com), which is the client I happen to know that I have used when absolutely forced to use IRC, and managed to connect to `irc.ergo.net`. I used port 6697 instead of 6667 to get an SSL connection, which I as a user just had to know. 

*Why are we forcing users in 2025 to choose whether to chat via plain text or SSL?*

Finally, I get in, and I try to list the channels on the server, and I get "users must be connected for 1 minute before listing channels". What type of user experience is that?

So finally I wait a minute and I get to list the channels, and immediately get horseshit like `#pissnet` on `irc.letspiss.net`. This is the type of shit you expect normal human users to tolerate when suggesting that they use an IRC server.

![[Pasted image 20250623135548.png]]

I connected to several channels, but didn't get history for any of them - not sure if that's because of the client I'm using?

I think I'm done here, IRC remains not recommendable to humans
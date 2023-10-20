https://github.com/lf-/clipper
https://jade.fyi/blog/announcing-clipper/

> The Clipper project allows you to easily debug HTTPS traffic of unmodified native applications, completely unprivileged (on Linux), without introducing any application-level tampering. It allows you to attach Chrome Dev Tools to most applications and view all their traffic as well as dump PCAPng files with included decryption keys, in one command.

----

> What if there _was_ one tool that was universal and could read any HTTP traffic with no configuration, for almost all apps? What if debugging a modern native app's HTTP traffic could be (almost) as easy as opening dev tools in a browser?

> I picked up the hammer and [built one](https://github.com/lf-/clipper). Here's a shell attached to Chrome Dev Tools, showing `curl` requests live:

----

> Announcing Clipper: a TLS-transparent HTTP debugging tool for native applications. With Clipper, you can attach Chrome DevTools to most native applications performing HTTP requests, with any HTTP library, with no configuration.

> This is done by sticking the app in a container, escrowing the keys using LD_PRELOAD tricks, intercepting the traffic of the container, then simply decrypting it.

- Jade, via [the toot announcing the project](https://hachyderm.io/@leftpaddotpy/110764798227834050)
Excellent article about how ANSI escapes work and how to use them: http://xn--rpa.cc/irl/term.html

a commenter on news.yc gives this page as the best guide to escape sequences they found: https://invisible-island.net/xterm/ctlseqs/ctlseqs.html (but note that it's aimed at xterm, not at any sort of standard, and other terminals may have more features)

Another gives: http://rtfm.etla.org/xterm/ctlseq.html

Useful tip from another:

> termfo[1] comes with a "termfo" CLI utility which – among other things – can group terminals by escape code; for example "termfo find-cap save_cursor" shows that almost all terminals use "\x1b7", with just a few very old ones using something different (full output is a bit long, but it's at [2]).
> 1: [https://github.com/arp242/termfo](https://github.com/arp242/termfo)
> 2: [https://pastebin.com/raw/pVHGR6aZ](https://pastebin.com/raw/pVHGR6aZ)
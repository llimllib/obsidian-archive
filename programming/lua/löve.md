---
updated: '2024-03-19T01:04:03Z'
created: '2024-03-19T01:04:03Z'
---
https://love2d.org/
https://love2d.org/wiki/Getting_Started

[@akkartik](https://merveilles.town/@akkartik)'s kids are playing [a neat-looking papercraft robot game](https://www.kiwico.com/us/store/dp/robot-coder-starter-kit/5555) and he wrote them a [little simulator](http://akkartik.name/post/rabbot) for it in löve, so I downloaded it to play with.

my getting started instructions, it's kind of painful:
- `brew install love`
- `love` is an unsigned binary, so open finder, go to `/Applications`, right-click on `love.app` and select `open`, then the button to open even though it's from an unknown developer
- Homebrew sets up a `love` shortcut for you, so now you can do `love rabbot-aa.love` and you'll be playing the game
	- If you installed the app manually, you can symlink the `love` binary from `/Applications/love.app/Contents/MacOS/love` to somewhere in your `PATH`
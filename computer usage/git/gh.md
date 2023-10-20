https://cli.github.com

I've begun relying on this tool when interacting with github, especially as it handles auth in nicer ways than google.

To set an alias: `gh alias set clone 'repo clone'` (I forget the `repo` part of that 100% of the time)

----

`gh run watch` is a handy command, it will give you a list of the actions currently running and let you watch it in the terminal until it's complete.

Ned Batchelder wasn't satisfied with that tool, so he created [watchgha](https://github.com/nedbat/watchgha). The main benefit is that it shows you all the workflows associated with a PR instead of just one. Here's the two running side by side, `gh run watch` on the left and `watchgha` on the right:

![[Pasted image 20230725102917.png]]

You get a denser display with `watch_gha`
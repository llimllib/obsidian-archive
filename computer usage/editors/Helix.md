https://github.com/helix-editor/helix

considering giving it a real try, it has a lot of features I like, and I especially like the idea of basically not configuring anything.

The thought of re-learning all those shortcuts that are hard-wired into my fingers though...

[Helix tutor](https://github.com/helix-editor/helix/blob/master/runtime/tutor)

[This page](https://github.com/helix-editor/helix/wiki/Migrating-from-Vim) gives some vim translations

the python support uses `pylsp`, install with `pip install python-lsp-server` [docs](https://docs.helix-editor.com/lang-support.html)

- delete a line: `xd`
- go to definition: `gd`
	- `ga` will go back to the last file, but I'm not sure that works quite like my vim `gh` does, which goes back up the goto stack
	- `ctrl-o` goes "backward on the jumplist", which seems to do what I want
- select lines
	- two options:
		- `v` to start a visual selection, `jjj` or any movement to move down, then `X` to "extend selection to line boundaries"
		- `xxx` will select the three lines beginning where the cursor is
- `config-open` to load the config file
- to replace all:
	- `x` to enter visual selection mode, `%` to select whole file, `s` to select a regular expression, `c` to change at the cursors, enter the replacement, `,` to remove the secondary cursors
	- `x%s<find><enter>c<replace><esc>,`
	- This seems a lot more cumbersome than `%s/something/other`?


- got an everforest theme from [this repo](https://github.com/CptPotato/helix-themes) and installed it by copying it into `~/.config/helix/themes`, then did `config-open` and changed `theme="everforest_dark_medium"`

- there's currently no equivalent to vim's `gq` command, which is kind of a deal-breaker for me at the moment. Got farther than I had before though!
	- <del>confirmed this on the helix matrix channel</del>
	- now it has [:reflow](https://docs.helix-editor.com/commands.html?highlight=reflow#commands) controlled by the [text-width](https://docs.helix-editor.com/configuration.html?highlight=reflow#editor-section) attribute ([here](https://github.com/helix-editor/helix/pull/2128) is the PR that implemented it)
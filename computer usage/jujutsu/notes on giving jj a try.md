---
created: 2024-10-21T14:23:08.182Z
updated: 2024-10-21T14:23:08.182Z
---
- add `.jj` to `~/.config/git/exclude` so git ignores `.jj` directories anywhere on my system
- clone my work repo to a directory on disk and switch into it, then run `jj git init --git-repo .`
	- This creates a `.jj` folder, but the backend format is still git
	- `jj` has a backend format but it's not v1 yet, and this allows you to still do get stuff as necessary (though it's not recommended)
	- I initially tried to clone from github, but that didn't work, so using regular git to pull from github and then init jj
- At work we develop on the `next` branch; `jj` warned me on init that that branch wasn't tracked
	- it offered me the `jj bookmark track next@origin` command, so I ran it
	- I'm vaguely aware that a bookmark corresponds to git's idea of a branch, but that's about it
- it warned me about not having a user and email configured, and offered commands to set them
	- `jj config set --user user.name "Bill Mill" && jj config set --user user.email "bill@billmill.org"`
- Then, it warned that I needed to set the current commit to my user
	- `jj` always has you "in a commit" even when you haven't done anything; there's no such thing as untracked changes in a `jj` world I guess
	- So, finally, I'm in a checkout of my repo at HEAD:
```
$ jj describe --reset-author --no-edit
Working copy now at: yynmmqzs 500ca078 (empty) (no description set)
Parent commit      : kuktztlw 483b19ff next | fix(sidebar): normalize child page data when checking to expand parent (#13072)
```

---
created: 2026-01-12T21:41:46.126Z
updated: 2026-01-12T21:41:46.126Z
---
I made more progress on [mdriver](https://github.com/llimllib/mdriver) (neé [[mdstream - a vibecoding experiment|mdstream]]), enough that I'm now [using it in my dotfiles](https://github.com/llimllib/personal_code/blob/master/homedir/.zshrc#L327-L333) to parse output from Simon's [[llm]] tool.

One thing I figured out was that I should work with [[How I use git worktrees|worktrees]] just like I do in other repositories, to help keep features separate. To support this, I added `.claude` to the list of untracked files I copy to new worktrees in [my worktree script](https://github.com/llimllib/personal_code/blob/master/homedir/.local/bin/worktree).

Adding them was `git config --global --add worktree.untrackedfiles ".claude"`

I looked briefly into having my `worktree` script tell `claude` that the newly-created worktree was trusted, so that you didn't have to say so every time you start `claude` in a new worktree, but unfortunately it doesn't seem like there's a reasonable way to do so.

Version `0.8.0` of `mdriver` has added:

- kitty image support
- hr support
- some basic HTML support
- fixed width
- more language support for syntax highlighting 
	- thanks to [two-face](https://crates.io/crates/two-face), which packages work done by [bat](https://github.com/sharkdp/bat/)
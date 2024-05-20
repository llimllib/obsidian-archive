---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
Oftentimes I create branches or worktrees and they don't end up getting pushed to remote and I forget about them. Alternatively, they do get pushed and I forget to prune them. Here's how to list them, and optionally to remove them.

## List all branches whose upstream has been removed

```bash
git branch --format="%(refname:short) %(upstream:track)" | 
    grep "\[gone\]"
```

- `git branch --format="%(refname:short) %(upstream:gone)"` lists the name and upstream status of each branch:
	```bash
	$ git branch --format="%(refname:short) %(upstream:track)"
	TheZoc/master [gone]
	gh-pages origin/gh-pages
	master origin/master
	```
	- The clever bit here is that `track` target, that tells us the status of the remote branch that the local branch is tracking
	- `man git-for-each-ref` tells us:

> `upstream` additionally respects `:track` to show `[ahead N, behind M]`... prints `[gone]` whenever unknown upstream ref is encountered.

- the branches we want are the ones which are `[gone]`:
```bash
$ git branch --format="%(refname:short) %(upstream:track)" | 
    grep "\[gone\]"
TheZoc/master [gone]
```
- Finally, you can give this command an alias like `git gone`:
```bash
git config --global alias.gone '!git branch --format="%(refname:short) %(upstream:track)" | grep "\[gone\]"'
```

## Remove all branches whose upstream has been removed

To remove them, pull out the branch name and use `xargs` to remove the branches:

```bash
git branch --format="%(refname:short) %(upstream:track)" | 
    grep "\[gone\]" |
    cut -f1 -d " " |
    xargs -I{} git branch -D {}
```

for example:

```bash
$ git branch --format="%(refname:short) %(upstream:track)" | 
    grep "\[gone\]" | 
    cut -f1 -d " " |
    xargs -I{} git branch -D {}
Deleted branch TheZoc/master (was 3d7b0ae).
```

You might alias this one to `git rm-gone`:

```bash
git config --global alias.rm-gone '!git branch --format="%(refname:short) %(upstream:track)" | grep "\[gone\]" | cut -f1 -d " " | xargs -I{} git branch -D {}'
```

- Aug 31 2023: Note improved to use the `track` option thanks to [Chris Adams](https://thepit.social/@acdha/110981824870247574) 
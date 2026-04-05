---
created: 2026-04-05T17:22:31.274Z
updated: 2026-04-05T17:22:31.274Z
---
I released [[git-ls]] version `5.4.0` with a fix and a new feature

## fix: rename handling

`git-ls` was not handling renamed files properly, because it was looking for the updated file name when the log only has the old file name.

It's been fixed to properly handle renames and copies in [#38](https://github.com/llimllib/git-ls/pull/38)

## feature: nerdfont

I've been using `git` 's `--porcelain` represenatation for changes; two columns, `M` for modified, `R` for renamed, `A` for added, `I` for ignored.

I wondered if there might be more useful terminal representations available, so [I made an experimental](https://github.com/llimllib/git-ls/pull/39) `--nerdfont` flag that uses nerd font icons instead.

New above, old below:

![[Pasted image 20260405132612.png]]

Let me know if you care about it one way or the other!
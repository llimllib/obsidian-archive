---
created: 2026-04-06T12:59:38.776Z
updated: 2026-04-06T12:59:38.776Z
---
I released [[git-ls]] version `5.4.0` with a fix and a new feature; upgrade with `brew upgrade llimllib/git-ls/git-ls` or download a release [from github](https://github.com/llimllib/git-ls).

`git-ls` is a combination file list and git status that I use instead of `git status` most of the time.

## fix: rename handling

`git-ls` was not handling renamed files properly, because it was looking for the updated file name when the log only has the old file name.

It's been fixed to properly handle renames and copies in [#38](https://github.com/llimllib/git-ls/pull/38)

## feature: nerdfont

I've been using `git` 's `--porcelain` represenatation for changes; two columns, `M` for modified, `R` for renamed, `A` for added, `I` for ignored.

I wondered if there might be more useful terminal representations available, so [I made an experimental](https://github.com/llimllib/git-ls/pull/39) `--nerdfont` flag that uses nerd font icons instead.

New above, old below:

![[Pasted image 20260405132612.png]]

Let me know if you care about it one way or the other!
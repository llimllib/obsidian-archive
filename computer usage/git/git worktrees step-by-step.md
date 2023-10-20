https://infrequently.org/2021/07/worktrees-step-by-step/

I use worktrees, but without the `bare` repo setup described here. May want to look into using it with the `gitdir:` thing I had never heard of, instead of using the `MAIN_BRANCH` [hack I've been using](https://github.com/llimllib/personal_code/blob/master/homedir/.local/bin/rmtree#L7).

Docs on `gitdir:` are [here](https://git-scm.com/docs/git-config#Documentation/git-config.txt-codegitdircode) and [here](https://git-scm.com/docs/gitrepository-layout) and probably in some more places

Found via [this piece](https://morgan.cugerone.com/blog/how-to-use-git-worktree-and-in-a-clean-way/), which has a [companion on fetching remote branches](https://morgan.cugerone.com/blog/workarounds-to-git-worktree-using-bare-repository-and-cannot-fetch-remote-branches/) which is apparently a shortcoming of the bare repository approach.

------

I tried to do this and I found the bare repository not to work very well for me at all - it does not want to list remote branches and just generally seems to be a pain to work with. I prefer the tooling I've built.

- [rmtree](https://github.com/llimllib/personal_code/blob/master/homedir/.local/bin/rmtree)
- [worktree](https://github.com/llimllib/personal_code/blob/master/homedir/.local/bin/worktree)

----

https://spin.atomicobject.com/2021/02/23/git-worktrees-untracked-files/

A neat hack! if you do `cp -Rc node_modules ../some_branch/` on a mac, APFS will create a copy-on-write version of your `node_modules` directory; this is something I've wanted for a long time.

> A copy-on-write (COW) clone duplicates an existing file without actually copying its contents on disk immediately. This is similar to a traditional hard link, except that if you modify a hard-linked file, the original file will be modified as well. But a COW clone copies the original if and only if it is written to (hence, “copy on write”).
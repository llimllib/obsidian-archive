---
created: 2026-01-28T13:33:46.359Z
updated: 2026-01-28T13:33:46.359Z
---
I realized recently that [`git-ls`](https://github.com/llimllib/git-ls) wasn't showing deleted files, so I have updated it to include deleted files in the listing.

![[Pasted image 20260128084607.png]]

Let me know if you like the look or want something different!

(I'm not actually removing the unlicense, just testing)

`git-ls` is a git status that shows you every file in your repository and its status, presented beautifully and with hyperlinks so you can click on the files to open them in your editor or the author and commit message to go to github.

Install it with `brew upgrade llimllib/git-ls/git-ls` or upgrade to 3.6.0 with `brew upgrade llimllib/git-ls/git-ls`
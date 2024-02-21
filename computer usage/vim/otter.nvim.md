https://github.com/jmbuhr/otter.nvim/
https://github.com/jmbuhr/otter.nvim/blob/main/doc/otter.nvim.txt

> Otter.nvim provides lsp features and a code completion source for code embedded in other documents

When messing around with [[Observable Framework]] I really missed having code completion available in the markdown docs you end up writing.

Setting up otter.nvim lets me do autocompletion inside fenced code blocks in markdown documents.

It's not perfect, because often you are writing javascript inside HTML inside the markdown block, and that doesn't work, but it's a pretty big improvement with a reasonably low cost.

Here's what it looks like, editing a plot inside a javascript code block in a markdown document:

![[Pasted image 20240221143205.png]]

It was reasonably easy to add it to my vim config: [commit 1](https://github.com/llimllib/personal_code/commit/51e4e177) [commit 2](https://github.com/llimllib/personal_code/commit/36192827)
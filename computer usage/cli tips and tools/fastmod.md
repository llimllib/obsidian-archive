---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/facebookincubator/fastmod

> `fastmod` is a fast partial replacement for [codemod](https://github.com/facebook/codemod). Like `codemod`, it is a tool to assist you with large-scale codebase refactors, and it supports most of `codemod`'s options. `fastmod`'s major philosophical difference from `codemod` is that it is focused on improving the use case "I want to use interactive mode to make sure my regex is correct, and then I want to apply the regex everywhere".

An example query is, if you want to replace `import type { Version }` everywhere in your codebase with `import type { VersionDocument }`, you might run:

`fastmod --extensions js,ts,tsx,jsx '\{ Version \}' '{ VersionDocument }' .`

(note that the first argument is a regular expression, and the second a literal string - so the braces need to be escaped in the first argument but not in the second)

By default, the tool will ignore hidden files; pass `--hidden` to match them.

The really nice thing about it, to me, is that it presents you with each change before it makes it, which is very helpful when creating these sorts of replacements. Often I find that I have to do a loop of making a project-wide replacement with sed, then checking the results with git, undoing the changes, and repeating until I finally have it right.
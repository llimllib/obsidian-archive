https://github.com/alexpovel/srgn

> A `grep`-like tool which understands source code syntax and allows for manipulation in addition to search.

> Like `grep`, regular expressions are a core primitive. Unlike `grep`, additional capabilities allow for **higher precision**, with **options for manipulation**. This allows `srgn` to operate along dimensions regular expressions and IDE tooling (_Rename all_, _Find all references_, ...) alone cannot, complementing them.

> `srgn` is organized around _actions_ to take (if any), acting only within precise, optionally **language grammar-aware**_scopes_. In terms of existing tools, think of it as a mix of [`tr`](https://www.gnu.org/software/coreutils/manual/html_node/tr-invocation.html#tr-invocation), [`sed`](https://www.gnu.org/software/sed/), [ripgrep](https://github.com/BurntSushi/ripgrep) and [`tree-sitter`](https://tree-sitter.github.io/tree-sitter/), with a design goal of_simplicity_: if you know regex and the basics of the language you are working with, you are good to go.

Like [[fastmod]], but with [[tree-sitter]] instead of regular expressions.

Available on homebrew

see also: [[comby]], [[tree-grepper]], [[tbsp]]
---
updated: 2024-06-06T14:17:12.314Z
created: 2023-10-20T13:54:09Z
---
https://github.com/ibraheemdev/modern-unix

> A collection of modern/faster/saner alternatives to common unix commands. 

Of this list, I use and recommend:

- [[bat]]: `cat` with syntax highlighting and line numbers
- delta: much better git diff output
- [[fd]]: an improved `find`
- [[ripgrep]]: a cornerstone of my workflow, an improved `grep`
- [[fzf]]: general purpose fuzzy finder. Its most useful feature for me is searching my command line history quickly and with a good UI
- [[jq]]: pull apart json, and build it up if necessary. Hugely useful in shell scripts with curl
- [[hyperfine]]: benchmark programs from the command line

on that list, I tried and didn't like:
- broot: seems like there's cool functionality in there, but I ultimately couldn't make it work like I wanted and it seemed too opinionated
- httpie/curlie/xh: neat tools but I'm fine with how `curl` works

on that list that I'm interested in:
- [sd](https://github.com/chmln/sd): I have suffered at the hands of attempting to write cross-platform sed. It stinks and I don't want to do it any longer
- [dust](https://github.com/bootandy/dust): du with modern touches
- [duf](https://github.com/muesli/duf): df with modern touches

not on that list but I use and is relevant:
- [atuin](https://atuin.sh/): keep your command history in a sqlite database
- [erdtree](https://github.com/solidiquis/erdtree): a better `tree`
- [doggo](https://github.com/mr-karan/doggo): a better `dig`
	- that list has `dog`, but doggo is a rewrite that I prefer
- [xsv](https://github.com/BurntSushi/xsv): manipulate csv files at the command line
- [hexyl](https://github.com/sharkdp/hexyl): a better `xxd`
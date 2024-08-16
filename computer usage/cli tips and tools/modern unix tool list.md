---
created: 2024-08-16T13:45:57.633Z
updated: 2024-08-16T13:45:57.633Z
---
For the purposes of this list, a tool is "modern" if it replaces a tool that you're likely to find in a base debian install.

I wish that the selection of CLI tools we provide with operating systems and broadly call "unix" would update itself much more frequently, but it doesn't, so you have to find updates where you can. Here are some tools I like:

- [atuin](https://atuin.sh/): keep your command history in a sqlite database
- [[bat]]: `cat` with syntax highlighting and line numbers
- [delta](https://github.com/dandavison/delta): much better git diff output
	- I often use this where you might use `diff` as well, it's great
- [doggo](https://github.com/mr-karan/doggo): a better `dig`
	- It doesn't do _everything_ dig does, but the bits it does, it does bettter
- [dust](https://github.com/bootandy/dust): du but faster and with nicer output
- [duf](https://github.com/muesli/duf): df with modern touches
- [erdtree](https://github.com/solidiquis/erdtree): a better `tree`
- [[fd]]: an improved `find`
- [[fzf]]: general purpose fuzzy finder. Its most useful feature for me is searching my command line history quickly and with a good UI
- [[hyperfine]]: benchmark programs from the command line
- [hexyl](https://github.com/sharkdp/hexyl): a better `xxd`
- [[jq]]: pull apart json, and build it up if necessary. Hugely useful in shell scripts with curl
- [[ripgrep]]: a cornerstone of my workflow, an improved `grep`
- [qsv](https://github.com/jqnatividad/qsv): manipulate csv files at the command line

Some tools I tried and didn't like:
- broot: seems like there's cool functionality in there, but I ultimately couldn't make it work like I wanted and it seemed too opinionated
- httpie/curlie/xh: neat tools but I'm fine with how `curl` works

This list originated at [[modern unix tools]], but I've moved it here so I can add to it as I find things.



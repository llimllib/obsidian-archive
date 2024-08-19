---
created: 2024-08-16T14:03:07.403Z
updated: 2024-08-19T18:10:52.725Z
---
For the purposes of this list, a tool is "modern" if it replaces a tool that you're likely to find in a base debian install.

I wish that the selection of CLI tools we provide with operating systems and broadly call "unix" would update itself much more frequently, but it doesn't, so you have to find updates where you can. Here are some tools I like:

- [atuin](https://atuin.sh/): keep your command history in a sqlite database
- [[bat]]: `cat` with syntax highlighting and line numbers
- [concurrently](https://www.npmjs.com/package/concurrently): run programs in parallel, and print their output in a pleasing way
	- it's hard to explain how nice this program is; I often use it when I want to run a web server and a database, and see both of their output together; it can give each program its own color so you can see at a glance what is logging
	- it's kind of shocking how hard it is to replace this tool with standard unix tools
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
- [[jless]]: interactively fold and unfold json documents
	- very helpful for working with large json documents
	- can output `jq` filters, making the two pair nicely
- [[ripgrep]]: a cornerstone of my workflow, an improved `grep`
- [qsv](https://github.com/jqnatividad/qsv): manipulate csv files at the command line

On my radar but haven't gotten to stick yet:
- [eza](https://github.com/eza-community/eza)
	- so far, `ls -FG --hyperlink=auto --color=auto` has been Good Enough™ for me

Some tools I tried and didn't like:
- broot: seems like there's cool functionality in there, but I ultimately couldn't make it work like I wanted and it seemed too opinionated
- httpie/curlie/xh: neat tools but I'm fine with how `curl` works

This list originated at [[modern unix tools]], but I've moved it here so I can add to it as I find things.



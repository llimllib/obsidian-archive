---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
The best tool I know of for recording sessions is [asciinema](https://asciinema.org/).

The CLI is downloadable with `brew install asciinema`

You can record a program's output with `asciinema rec -c <command> output_filename.rec`

You can then upload it to asciinema.org or convert the recording to a gif with [agg](https://github.com/asciinema/agg)

[here](https://github.com/llimllib/personal_code/blob/master/misc/advent/2022/12/search.gif) is an example gif I made with curses and asciinema of a maze search from an advent of code problem.

_update Jun 24 2024_: [vhs](https://github.com/charmbracelet/vhs) is a neat-looking scriptable version of asciinema. It says:

> Write terminal GIFs as code for integration testing and demoing your CLI tools.

and demonstrates a short script that results in this output:

![[Pasted image 20240624081756.png]]
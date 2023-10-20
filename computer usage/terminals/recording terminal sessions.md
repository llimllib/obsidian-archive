The best tool I know of for recording sessions is [asciinema](https://asciinema.org/).

The CLI is downloadable with `brew install asciinema`

You can record a program's output with `asciinema rec -c <command> output_filename.rec`

You can then upload it to asciinema.org or convert the recording to a gif with [agg](https://github.com/asciinema/agg)

[here](https://github.com/llimllib/personal_code/blob/master/misc/advent/2022/12/search.gif) is an example gif I made with curses and asciinema of a maze search from an advent of code problem.
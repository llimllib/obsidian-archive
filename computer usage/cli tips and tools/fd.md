---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/sharkdp/fd

> A simple, fast and user-friendly alternative to 'find'

I like this program a lot better than [[find]]

notable options:

- `-e`, `--extension`: filter results by the given file extension. Can give multiple
- `-E`, `--exclude`: exclude files/directories that match the given pattern
- `-g`, `--glob`: use glob syntax instead of regex
- `-H`, `--hidden`: include directories and files starting with  a `.` in the search
- `-t`, `--type`: search by type. `f` = file, `d` = directory (more options, but those are the two I use)
- `-u`, `--unrestricted`: include ignored and hidden files in the search
- `-x`, `--exec`: execute a command for each result in parallel
	- replaces a lot of `find | xargs` pipes; an example from the docs is, to convert all `*.jpg` to `*.png` with imagemagick: 
		- `fd -e jpg -x convert {} {.}.png`

-----

find all empty files and delete them:

`fd -t empty -t file -x rm`

(find all empty files, execute rm)

list all dotfiles in the home directory, without recursing:

`fd -d1 -u '^\.' ~`

(`-d1` to not recurse, `-d` == `--depth`. `-u` as above)
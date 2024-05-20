---
updated: '2024-03-18T14:31:01Z'
created: '2023-10-20T13:54:09Z'
---
## print a table

to print a table, [[neovim]] has a handy function `vim.inspect`. I used it to inspect a table of colors like so:

`:lua print(vim.inspect(require("mini.base16").mini_palette("#252A39", "#CBCCC6", 75)))`

## open the output of a command in a split

`:new | 0read ! ls $HOME`

The `0` in `0read` is a range argument; it says to insert the output of the following command at the start of the buffer

## viewing man pages

`:Man tmux` will open the man page with a nice format
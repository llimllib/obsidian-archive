---
updated: 2025-03-05T13:31:42.879Z
created: 2023-10-20T13:54:09Z
---
https://sw.kovidgoyal.net/kitty/

> _The fast, feature-rich, GPU based terminal emulator_

# opening files with clicks

- open actions docs: https://sw.kovidgoyal.net/kitty/open_actions/
- launch docs: https://sw.kovidgoyal.net/kitty/launch/
- sent text docs: https://sw.kovidgoyal.net/kitty/remote-control/#kitten-send-text
- create a file `~/.config/kitty/open-actions.conf`:
```
# cd into the clicked directory and list its contents
protocol file
mime inode/directory
action send_text normal,application cd ${FILE_PATH}\rls\r

# If a line number is clicked (indicated by presence of a fragment), jump to
# that line number in an editor. Use `rg --hyperlink-format=kitty` to use this
# feature
protocol file
fragment_matches [0-9]+
action send_text normal,application $EDITOR +${FRAGMENT} ${FILE_PATH}\r

# Open text files without fragments in the editor
protocol file
mime text/*,application/*
action send_text normal,application $EDITOR ${FILE_PATH}\r

# some files were matching by extension to opening with system stuff. Add to
# this extension list to open more types of files with vim
protocol file
ext yml,json,ts,tsx,jsx,py,sh,bash,rb,tf,dot
action send_text normal,application $EDITOR ${FILE_PATH}\r

# Dockerfile doesn't match by extension or mime type, so use a regex on the
# name
protocol file
url Dockerfile
action send_text normal,application $EDITOR ${FILE_PATH}\r

# Open image files with icat
protocol file
mime image/*
action send_text normal,application icat ${FILE_PATH}\r
```

- run `gls --hyperlink=auto` on a mac, or `ls --hyperlink=auto` if you have gnu ls, and try clicking on files to see what happens
	- click on a directory to enter that directory
	- run `rg --hyperlink-format=kitty <something>`, then click on a line number, and you should get brought right to that line
- [here's the commit](https://github.com/llimllib/personal_code/commit/4493a7e47fff527d1e0f9eed9ea23749b9a2709a) where I introduced it into my dotfiles
	- you can [configure delta to use hyperlinks too](https://github.com/llimllib/personal_code/commit/3afdcdef3a936d283dea4cea6281bb3c7de24895)

## opening files from finder

[this github issue comment](https://github.com/kovidgoyal/kitty/issues/4460#issuecomment-2677434820) shows how you can create an Automator "application" that will find your kitty app, add a tab, and open a file with it.

Automator is just a crazy app, I don't know how apple ever expects anybody to use it, but I tried it out and this works perfectly.
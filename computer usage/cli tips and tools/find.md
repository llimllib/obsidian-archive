---
updated: '2024-03-05T22:03:41Z'
created: '2023-10-20T13:54:09Z'
---
Find all files in the current directory that end in `*.js` or `*.ts`, but ignore paths containing `node_modules`:

`find . \( -iname '*.js' -o -iname '*.ts' \) -not -path '*node_modules*'`

Equivalent [[fd]] command:

`fd -g --exclude node_modules '*.{ts,js}'`

or, `fd --exclude node_modules '\.(js|ts)$'`, using regex instead of glob search.

`-E` is a shortcut for `--exclude`

**update** You can actually do better in `find` by using the `-iregex` flag:

`find -E . -iregex '.*\.(ts|js)' -not -iregex '.*node_modules.*'`

note that in the regular expressions given to find, you're matching against the _full path_ not the filename as you are in `fd`.

-----

Find all empty files and delete them:

`find . -type f -empty -print -delete`
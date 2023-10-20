Find all files in the current directory that end in `*.js` or `*.ts`, but ignore paths containing `node_modules`:

`find . \( -iname '*.js' -o -iname '*.ts' \) -not -path '*node_modules*'`

Equivalent [[fd]] command:

`fd -g --exclude node_modules '*.{ts,js}'`

or, `fd --exclude node_modules '\.(js|ts)$'`, using regex instead of glob search.

`-E` is a shortcut for `--exclude`

-----

Find all empty files and delete them:

`find . -type f -empty -print -delete`
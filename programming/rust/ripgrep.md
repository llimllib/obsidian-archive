https://github.com/BurntSushi/ripgrep

The best grep tool

-----

Find each line of code referencing `req.app.local`, print it out in context, and let bat syntax color the output:

`rg -N -I -C10 req.app.local | bat -p -f -l ts`

Unfortunately in this case it won't highlight the actual match. Bat says:

> If an input file contains color codes or other ANSI escape sequences or control characters, `bat` will have problems performing syntax highlighting and text wrapping, and thus the output can become garbled. When displaying such files it is recommended to disable both syntax highlighting and wrapping by passing the `--color=never --wrap=never` options to `bat`.

whoa wait but there's [batgrep](https://github.com/eth-p/bat-extras/blob/master/doc/batgrep.md) in `bat-extras` ([source](https://github.com/eth-p/bat-extras)), which basically just performs that wrapping for you! `brew install bat-extras` to get it on a mac. Neat.

-----

Cat a file to the terminal but highlight text that matches a regex:

`rg -N --passthru <regex> <file>`

----

Given a file which has errors like:

`6:16  error  '@types/config' should be listed in the project's dependencies, not devDependencies  import/no-extraneous-dependencies`

If you want to filter a bunch of those lines and others down to the packages that need to be listed, you can do:

`rg -o "'(.*)' should be listed in the project" /tmp/b.out -r '$1' | sort | uniq`

- `-o` to only output the match
- the regex captures the package name in a named group
- `-r` replaces the output with the captured group
- sort sorts the packages and unique de-duplicates them
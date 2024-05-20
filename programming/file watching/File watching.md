---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
I usually use [modd](https://github.com/cortesi/modd) (with [[devd]]), but it's not maintained.

[watchexec-cli](https://lib.rs/crates/watchexec-cli) looks like a good simple replacement for many of my use cases

https://github.com/watchexec/watchexec

Paul Smith wrote a [simple bash reloader](https://github.com/paulsmith/reloader.sh) that wraps [fswatch](https://emcrisostomo.github.io/fswatch/)

[entr](https://github.com/eradman/entr) is another

- Facebook's [watchman](https://facebook.github.io/watchman/)
	- To run a command when a js or ts files changes, use `watchman-make`, Example:
	- `watchman-make -p '**/*.js' '**/*.ts' --run 'npx jest'`
	- [docs](https://facebook.github.io/watchman/docs/watchman-make)
	- does not seem to support extended glob syntax, so you can't use `**/*.{js,ts}` as the value provided to the `-p` option

- [crodjer/watchman](https://github.com/crodjer/watchman) same name, separate projects. This is a bash file that depends on `inotifywait`, so is linux-only. I mention it only because it is confusing that there are two projects with the same name

[notify](https://pkg.go.dev/github.com/rjeczalik/cmd/notify?utm_source=godoc) is a go command using the same library that modd depends on

[watchfiles](https://github.com/samuelcolvin/watchfiles): Simple, modern and high performance file watching and code reload in python.
- both a python lib and a [cli tool](https://watchfiles.helpmanual.io/cli/)
	- the cli is very python-oriented
	- `watchfiles "go test" **/*.go` works as advertised though, and runs `go test` when any go file changes
	- it has a reasonably low file limit, which can be a problem in node setups with node_modules
		- In that case, use something like:
		- `watchfiles "npx jest" $(fd -g --exclude node_modules "*.{ts,js}"`

[reflex](https://github.com/cespare/reflex) is a go file watcher that looks pretty good, supports config files

[ochinchina/supervisord](https://github.com/ochinchina/supervisord) is a reimplementation of python supervisord in go. Includes the capability to restart the service when a file changes (`restart_cmd_when_file_changed`, though that's not its main focus)

[gajus/turbowatch](https://github.com/gajus/turbowatch/) is a scriptable node file watcher built on top of watchman. "Turbowatch adds a layer of abstraction for orchestrating task execution in response to file changes (shell interface, graceful shutdown, output grouping, etc)."

[mitranim/gow](https://github.com/mitranim/gow) "**Go** **W**atch: missing watch mode for the `go` command. It's invoked exactly like `go`, but also watches Go files and reruns on changes."
- only for go
- based on [rjeczalik/notify](github.com/rjeczalik/notify), like modd does

[wtetsu/gaze](https://github.com/wtetsu/gaze) is a file watcher that is optimized around running files immediately after you save them; by default it tries to guess how to run the file.
- so if you run `gaze .` and edit a file `something.py`, it will run `python something.py` every time you save, by guessing that you want to run the file with `python`
- you can customize the mapping with the `-c` option
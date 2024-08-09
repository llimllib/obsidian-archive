---
created: 2024-08-09T13:26:26.812Z
updated: 2024-08-09T13:26:26.812Z
---
I needed to figure out how to debug the `git` binary to figure out exactly what it was doing, and I thought I'd share the setup because it took me a little while to get going.

# Prerequisites

- install [visual studio code](https://code.visualstudio.com/)
- install the [microsoft C/C++ extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools)
- you will need to have `lldb`, the llvm debugger available on your system. 
	-  To see if you have `lldb` available, do `which lldb`; as long as it prints a path and not `lldb not found`, you're good to go
	- The most common way to get it installed is to install `Xcode` from the app store or the `Xcode Command Line Tools` which can be installed with `xcode-select --install`
	- You may also install it with homebrew by doing `brew install llvm`. Be aware though that brew will not link it by default, so you'll have to figure out how to tell vs code to use it

# Building git

- Clone the git repository: `git clone https://github.com/git/git`
- Change into the cloned directory: `cd git`
- Set some build variables by creating a file called `config.mak`. It should have exactly these contents:
	```makefile
	DEVELOPER=1
	CFLAGS+= -O0
	```
	- A command you might use to make this file: `printf 'DEVELOPER=1\nCFLAGS+= -O0' > config.mak`
	- see [the Makefile](https://github.com/git/git/blob/25673b1c476756ec0587fb0596ab3c22b96dc52a/Makefile#L556) for more info on what `DEVELOPER` does
	- the `CFLAGS` variable provides a flag to the C compiler to build a binary with no compiler optimizations; traditionally `O3` means "the most optimizations" and `O0` means "no optimizations"
		- [clang documentation](https://clang.llvm.org/docs/CommandGuide/clang.html#code-generation-options) on optimization options
- `make -j4`
	- The `-j` argument to make tells it how much parallelism it can use. It speeds up the build by increasing parallelism; you can use more if you have more CPUs, or less if you have fewer. The build doesn't take very long though so it's not a big deal.
- When this completes successfully, you should have a bunch of new binaries in your git directory, such as `git`, `git-add`, `git-am`, etc

# Debugging git
- make a `.vscode` directory: `mkdir .vscode`
- open the git directory with visual studio code: `code .`
- create a file in the `.vscode` directory called `launch.json` that tells vs code how to start `git` for debugging. Its contents should be:
	```json
    {
      "configurations": [
	    {
		  "name": "debug git",
		  "type": "cppdbg",
	      "request": "launch",
	      "program": "${workspaceFolder}/git",
	      "args": ["status"],
	      "cwd": "${workspaceFolder}",
		  "externalConsole": false,
		  "MIMode": "lldb"
	    }
      ]
    }
	```
	- Note that we're passing `status` as an argument; the first command we're going to debug is `git status`. To debug other commands, you'll want to change the `args` option
	- See the [documentation](https://code.visualstudio.com/docs/cpp/launch-json-reference) for information on these configuration options and what additional flags are available
- Open the `builtins/commit.c` file in the editor
- Set a breakpoint on the first line inside the `cmd_status` function; in my current version of git, that's located at line 1504
	- To set a breakpoint, click on the left gutter, just to the left of the line numbers; you should see a red dot appear. Once a breakpoint is set, the debugger will stop when it reaches that location, allowing you to control execution of the program
		- [here is VS Code's documentation](https://code.visualstudio.com/docs/editor/debugging#_breakpoints) on how to set breakpoints
	- Annoyingly, setting a breakpoint at the function name doesn't seem to work for me, so I have to set a breakpoint _inside_ the function or else the program doesn't break
		- If you really want to do this, in the command palette there's an action called `Add Function Breakpoint`, which created a function breakpoint that I could type `cmd_status` into, and that did break on the function invocation
	- The `builtins` directory contains most of the high-level git UI code
	- git subcommands will have a function name `cmd_<command name>`; check out `cmd_log` or `cmd_commit` for other examples
- Switch to the `Run and Debug` tab of VS code
- click on `start debugging`, the green arrow located at the top left of the window, or press F5 to do the same thing.
	- alternatively, open your command palette with `⇧⌘P`, type `Debug`, and select `Debug: Select and Start Debugging`, then select `debug git`

If all goes well, you should now be controlling the execution of git inside VS code! Go ahead and dig in to try and understand what's going on.

I might write more about what it is that's going on in there, but I'm not sure - let me know if you would like to understand some part of it better.
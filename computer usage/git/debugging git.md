[this gist is a helpful resource](https://gist.github.com/phil-blain/17c67740bd26e66f4851fe0c07230ea4)

1. `./configure`
2. `printf 'DEVELOPER=1\nCFLAGS+= -O0\n' > config.mak`
3. `make`

on a mac: `GIT_DEBUGGER="lldb --" ./bin-wrappers/git <command> <args...>`

For example, let's debug `git log -1 --shortlog` and use `break set -n cmd_log` to set a breakpoint on the `cmd_log` function:

```
$ GIT_DEBUGGER="lldb --" ./bin-wrappers/git log -l --shortlog
(lldb) break set -n cmd_log
Breakpoint 1: where = git`cmd_log + 28 at log.c:882:2, address = 0x000000010008d014
(lldb) run
Process 62644 launched: '/Users/llimllib/code/tmp/git/git' (arm64)
Process 62644 stopped
* thread #1, queue = 'com.apple.main-thread', stop reason = breakpoint 1.1
    frame #0: 0x000000010008d014 git`cmd_log(argc=3, argv=0x000000016fdfe8b8, prefix=0x0000000000000000) at log.c:882:2
   879 		struct rev_info rev;
   880 		struct setup_revision_opt opt;
   881 	
-> 882 		init_log_defaults();
   883 		git_config(git_log_config, NULL);
   884 	
   885 		repo_init_revisions(the_repository, &rev, prefix);
Target 0: (git) stopped.
```

Alright! now we've got a debugger going, woo.

## aside: making clangd happy

I'm using [clangd](https://clangd.llvm.org/) as my LSP, and by default it can't find local header files.

To get it set up properly, I eventually found [this page](https://clangd.llvm.org/installation#project-setup) which points to the [bear](https://github.com/rizsotto/Bear) tool for generating a clangd config.

To use bear, I ran `make clean ; bear -- make`, which tells bear to instrument a `make` run and output a `compile_commands.json` file that tells `clangd` what flags to use and where to find header files.

Now I don't have squiggly red lines!


https://direnv.net/

After you've installed direnv, any directory containing a `.envrc` file will be executed when you enter that directory in your shell. Pairs well with [[basic commands]] for managing programming language environments.

This is super handy for loading secret values as environment variables in your programming projects.

For example, say you have an AWS token for your project that you want to keep secret, but make available to your program; you create a `.envrc` file in that directory with `direnv edit .`, and fill it in with these contents:

```
export AWS_TOKEN=DcCca124cedc212
```

save the file, exit your editor, and direnv will load that variable into the shell for you.

```shell
$ direnv edit .
direnv: loading /home/llimllib/test/.envrc
direnv: export +AWS_TOKEN
```

when you leave the directory, direnv will remove the variable from your environment:

```shell
$ cd ~
direnv: unloading
$ echo "aws token is now empty: <$AWS_TOKEN>"
aws token is now empty: <>
```

For security reasons, direnv won't execute a `.envrc` file until you tell it to do so with `direnv allow`:

```shell
$ mkdir test
$ echo "export AWS_TOKEN=blahblah" > test/.envrc
$ cd test
direnv: error /tmp/test/.envrc is blocked. Run `direnv allow` to approve its content

$ direnv allow
direnv: loading /tmp/test/.envrc
direnv: export +AWS_TOKEN
```

What direnv is actually doing is (roughly) starting up a new shell, executing the `.envrc` file, comparing the environment variables between the two, and importing the variables into your current session that are new.

That means that it is _not_ executing the `.envrc` file in your current shell session, which means that running a program that modifies your environment, like activating a python virtualenv might not work exactly like you expect it to.

If you try to activate a python virtualenv in a `.envrc`, `activate` will modify your environment to insert its own python on your `PATH` - this will work because `direnv` will import the update path. However, it also tries to modify your command line prompt  via `$PS1`, which is a local variable, and as such will not propagate back to your shell.

The [direnv wiki](https://github.com/direnv/direnv/wiki/Python#restoring-the-ps1) lists some workarounds, but they're fairly gross. I just live without the updated `PS1`.

There are some [common programming environment layouts](https://github.com/direnv/direnv/blob/master/man/direnv-stdlib.1.md#layout-go) available - for example if you add `layout node` to your `.envrc`, direnv will put `$PWD/node_modules/.bin` on your `PATH` when you enter the directory.
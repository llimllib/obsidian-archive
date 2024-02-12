I wanted to see how long the command `make lint-types` took with an environment variable present, so I tried this command and it failed:

```console
$ CI=true time make lint-types
zsh: parse error near `time'
```

I couldn't figure out why! It turns out that [time is a reserved word](https://www.zsh.org/mla/workers/2019/msg00876.html), and it only works as the first argument. This command is the proper way to spell what I was trying to spell:

```console
$ time CI=true make lint-types
```
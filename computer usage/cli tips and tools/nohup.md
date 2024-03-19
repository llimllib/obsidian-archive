To launch a process in the background, use a trailing `&`. This command launches a subshell in the background:

```shell
(sleep 5 && echo "done") &
```

If you close your current shell, that job will die.

One way to make the job stay alive even if you close your shell is to use `nohup`

```shell
nohup bash -c "sleep 5 && echo "done" >> /tmp/done" &
```

I had to change the subshell from `()` to `bash -c` because nohup doesn't work with subshell notation.

By default, `nohup` will send the output of the command to a file called `nohup.out`:

> If the standard output is a terminal, the standard output is appended to the file nohup.out in the current directory.

To avoid this, you can redirect your output somewhere. Here I've redirected it to a temp file:

`nohup bash -c "npm i && make dist webpack stylus" &> $(mktemp) &`
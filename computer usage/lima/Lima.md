https://github.com/lima-vm/lima

> The goal of Lima is to promote [containerd](https://containerd.io) including [nerdctl (contaiNERD ctl)](https://github.com/containerd/nerdctl) to Mac users, but Lima can be used for non-container applications as well.

`limactl start` to start a vm for lima to use

Now, `lima` drops me into a linux shell:

```
09:47 AM lexeme:~
$ lima
llimllib@lima-default:/Users/llimllib$
```

neat!

I'm not quite sure where the linux home drive lives:

```
llimllib@lima-default:/Users/llimllib$ uname -a
Linux lima-default 5.15.0-41-generic #44-Ubuntu SMP Thu Jun 23 11:20:13 UTC 2022 aarch64 aarch64 aarch64 GNU/Linux
llimllib@lima-default:/Users/llimllib$ cd
llimllib@lima-default:~$ pwd
/home/llimllib.linux
```

it sets up `/tmp/lima` and `/Users` as shareable directories by default

you can also run particular containers, utilizing `containerd`:

```
lima nerdctl run -d --name nginx -p 127.0.0.1:8080:80 nginx:alpine
```

`limactl list` to list the instances, `limactl stop <INSTANCE>` and/or `limactl DELETE <INSTANCE>` to kill it

`limactl stop` to stop the QEMU VM

I like it! But I'm not sure it will replace docker desktop for me, and also that it's the sort of thing I install and then six months later I'm like "what is this thing sucking up CPU" and oh yeah it's the VM thing I installed six months ago and forgot to use 🤷‍♂️
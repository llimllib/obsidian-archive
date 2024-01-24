https://www.bigbinary.com/blog/zsh-profiling

Inspired by [Larry Tratt](https://tratt.net/laurie/blog/2024/faster_shell_startup_with_shell_switching.html) linking to [Thorsten Ball](https://registerspill.thorstenball.com/p/how-fast-is-your-shell), I took a quick look at shell startup time this morning.

zsh has a built-in profiler, which is very handy. Before I ran it, my shell startup was about 373ms:

```
$ hyperfine --shell=none "zsh -i -c exit"
Benchmark 1: zsh -i -c exit
  Time (mean ± σ):     373.2 ms ±  13.3 ms    [User: 210.6 ms, System: 148.3 ms]
  Range (min … max):   364.0 ms … 409.5 ms    10 runs
```

When I ran it, I saw that `compinit`, which [initializes zsh's completion system](https://zsh.sourceforge.io/Doc/Release/Completion-System.html#Initialization), was taking most of that time:

```
$ ZDOTDIR=/tmp/profile_zshrc zsh
num  calls                time                       self            name
-----------------------------------------------------------------------------------
 1)    1          59.07    59.07   31.84%     59.07    59.07   31.84%  compdump
 2)    1         185.32   185.32   99.89%     54.74    54.74   29.51%  compinit
 3)  795          54.11     0.07   29.16%     54.11     0.07   29.16%  compdef
 4)    2          17.40     8.70    9.38%     17.40     8.70    9.38%  compaudit
 5)    3           0.20     0.07    0.11%      0.20     0.07    0.11%  add-zsh-hook
 6)    1           0.00     0.00    0.00%      0.00     0.00    0.00%  delta_sidebyside
```

So I searched (Kagi'd?) "slow compinit", and found that most of the time is taken up in parsing a dumpfile that doesn't change that often. So I replaced this line:

```
autoload -Uz compinit && compinit
```

with these ones, which will only run `compinit` without `-C` if it's been 24 hours since the dumpfile was last opened:

```
autoload -Uz compinit
for dump in ~/.zcompdump(N.mh+24); do
  compinit
done
compinit -C
```

And now my shell spawns much more quickly:

```
$ hyperfine --shell=none "zsh -i -c exit"
Benchmark 1: zsh -i -c exit
  Time (mean ± σ):      45.3 ms ±   3.5 ms    [User: 21.4 ms, System: 16.6 ms]
  Range (min … max):    42.2 ms …  64.6 ms    46 runs
```
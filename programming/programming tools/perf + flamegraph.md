`perf` Only works on linux, but: https://www.brendangregg.com/FlameGraphs/cpuflamegraphs.html#perf

Shows that to get a flamegraph of where a binary is spending its time, you can use steps like this:

```
# git clone https://github.com/brendangregg/FlameGraph  # or download it from github
# cd FlameGraph
# perf record -F 99 -a -g -- sleep 60
# perf script | ./stackcollapse-perf.pl > out.perf-folded
# ./flamegraph.pl out.perf-folded > perf.svg
# firefox perf.svg  # or chrome, etc.
```

I saw this in a thread about [[Zig]] performance, somebody used perf+flamegraph to analyze a program and notice that all its time was spent reading a file (was using an unbuffered read - 28 million syscalls intead of a few k) instead of performing useful work.
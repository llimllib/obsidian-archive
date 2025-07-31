---
created: 2025-07-31T20:19:42.316Z
updated: 2025-07-31T20:19:42.316Z
---
https://github.com/andrewrk/poop

Andrew Kelley's performance measurement tool, which outputs [more data](https://github.com/andrewrk/poop#comparison-with-hyperfine) than [[hyperfine]].

Unfortunately linux only as it relies on [[perf + flamegraph|perf]], however there is a [fork](https://github.com/verte-zerg/poop/tree/kperf-macos) which adds mac support. Andrew [will not be accepting mac support](https://github.com/andrewrk/poop/pull/70#issuecomment-3129965556) for the tool.

## building the mac fork

I tried and failed to build the mac fork with:

```bash
git clone https://github.com/verte-zerg/poop verte-zerg-poop
git switch kperf-macos
# make sure you have (at the time of this writing) zig 0.14.1
zig build --release=fast
cp zig-out/bin/poop ~/.local/bin/ # or wherever you want
```

sadly, that seems to compile correctly but die with `error: GetKpcAllCounters` whenever I try to use it

info about the fork via [this article about zig profiling tools on mac](https://blog.bugsiki.dev/posts/zig-profilers/) via [news.yc](https://news.ycombinator.com/item?id=44718211)
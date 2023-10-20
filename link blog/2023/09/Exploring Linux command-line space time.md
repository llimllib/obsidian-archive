https://fabiensanglard.net/st/index.html

> I was curious to explore how long a program takes to run, how much memory is used over time, and what processes/threads are spawned. To provide answers I wrote a tool, which I named st. Here are a few things I looked into.

> See details at the bottom if you are interested in how the tool works (and why I did not use time(1) and strace(1)).

Very cool graphs.

I've written a bit in the past about [tracking memory usage over a process' life](https://adhoc.team/2019/05/01/memory-measurement/), and I remain surprised that there isn't a standard tool for doing this very useful activity.

I'm tempted to write an equivalent that works on mac, using `eslogger` (see [[debugging os x]]) to track execs and `ps` to measure RSS (PSS is not available on macs if I understand correctly (but I linked to [this SO post](https://stackoverflow.com/questions/118307/a-way-to-determine-a-processs-real-memory-usage-i-e-private-dirty-rss/1954774#1954774) in the past which seems to say that you can use `vmmap` to get at least very close to something similar))
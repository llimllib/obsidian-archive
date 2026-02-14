---
created: 2026-02-14T14:29:56.692Z
updated: 2026-02-14T14:29:56.692Z
---
https://github.com/themattrix/bash-concurrent

> A Bash function to run tasks in parallel and display pretty output as they complete.

Rather than showing the output of the programs it runs, it stuffs them into `.logs/<timestamp>`

One thing it has that I like and would like to steal for [[crun]] (or a successor? Is that just a port and shouldn't add functionality?) is a notion of task dependencies:

(Thought: should that be a separate tool? `dep` specifies a dependency tree, then runs the tasks it needs with `crun` if necessary or just by themselves? Is that just `make`?)

> Start the medium task after the short task succeeds:

```bash
concurrent \
    - 'My long task'   sleep 10 \
    - 'My medium task' sleep 5  \
    - 'My short task'  sleep 1  \
    --require 'My short task'   \
    --before  'My medium task'
```

Its method of providing names is interesting, though it requires some acrobatics around the `-` specifier.
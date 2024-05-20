---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
I wanted to rename all `*.pushup` files in a file tree to `*.up`. Every time I have to do this, I figure out a loop or find/xargs invocation that works, then don't do it for long enough to forget how to do it.

Here's what I used this time (this expects [globstar](https://www.gnu.org/software/bash/manual/html_node/The-Shopt-Builtin.html) to be enabled):

```
for f in **/*.pushup; do git mv $f ${f%.pushup}.up; done
```

The `%` inside the parameter expansion tells bash to match `$f` up until it finds `.pushup`. [reference here](https://www.gnu.org/software/bash/manual/bash.html#Shell-Parameter-Expansion)
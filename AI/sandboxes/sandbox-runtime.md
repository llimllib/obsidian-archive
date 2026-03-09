---
created: 2026-03-09T12:55:19.037Z
updated: 2026-03-09T12:55:19.037Z
---
https://github.com/anthropic-experimental/sandbox-runtime

>  A lightweight sandboxing tool for enforcing filesystem and network restrictions on arbitrary processes at the OS level, without requiring a container. 

uses [[sandbox-exec]] on mac and [bubblewrap](https://github.com/containers/bubblewrap) on linux.

Can be used as a command line wrapper
---
created: 2026-04-06T12:59:38.727Z
updated: 2026-04-06T12:59:38.727Z
---
https://github.com/anthropic-experimental/sandbox-runtime

>  A lightweight sandboxing tool for enforcing filesystem and network restrictions on arbitrary processes at the OS level, without requiring a container. 

uses [[sandbox-exec]] on mac and [bubblewrap](https://github.com/containers/bubblewrap) on linux.

Can be used as a command line wrapper

There is a [pi extension](https://github.com/badlogic/pi-mono/blob/d9cfa115bed37c6036734ec3ab5ad1cbbda6f36a/packages/coding-agent/examples/extensions/sandbox/package.json) to bring it into pi (compare [[pi-sandbox]])
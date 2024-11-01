---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/zalando/go-keyring

> `go-keyring` is an OS-agnostic library for _setting_, _getting_ and _deleting_ secrets from the system keyring. It supports **OS X**, **Linux/BSD (dbus)** and **Windows**.

> go-keyring was created after its authors searched for, but couldn't find, a better alternative. It aims to simplify using statically linked binaries, which is cumbersome when relying on C bindings (as other keyring libraries do).

Similar to the [[programming/python/keyring]] library in python, I found it because [the gh cli started using it](https://github.com/cli/cli/pull/7043)
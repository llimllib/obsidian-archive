---
created: 2026-01-27T14:03:34.983Z
updated: 2026-01-27T14:03:34.983Z
---
For work, I needed to test a mac setup script which required a clean mac installation.

Rather than try to blow up my own computer and start fresh, I wanted to use a VM.

My first attempt was using [[tart]]. Install went smoothly:

```shell
brew install cirruslabs/cli/tart
tart clone ghcr.io/cirruslabs/macos-tahoe-base:latest tahoe-base
tart run --dir=setup-tree:~/project/setup-tree tahoe-base
```

With the `--dir` argument in place, tart mounted my directory to `/Volumes/My\ Shared\ Files/setup-tree` which is a bit of a weird directory but good enough.

Unfortunately, my setup script uses [[homebrew]], and brew ran so slowly in the VM that it wasn't able to succeed at installing a few packages.

For my next test, I'm trying out [[UTM]]
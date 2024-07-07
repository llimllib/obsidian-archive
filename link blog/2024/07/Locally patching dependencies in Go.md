---
created: 2024-07-07T15:15:48.780Z
updated: 2024-07-07T15:15:48.780Z
---
https://eli.thegreenplace.net/2024/locally-patching-dependencies-in-go/

A thorough (as always for Eli) writeup on how to locally modify a dependency to test behavior.

`node_modules` is generally awful, but this is one place where it's great: I frequently just hop into the code for one of my dependencies and change it or debug into it to see why it's doing something surprising.

It's a bit more tricky to do this in go, but only a bit as Eli shows here.
---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/ebitengine/purego

> A library for calling C functions from Go without Cgo.

> The [Ebitengine](https://github.com/hajimehoshi/ebiten) game engine was ported to use only Go on Windows. This enabled cross-compiling to Windows from any other operating system simply by setting `GOOS=windows`. The purego project was born to bring that same vision to the other platforms supported by Ebitengine.

> - **Simple Cross-Compilation**: No C means you can build for other platforms easily without a C compiler.
> - **Faster Compilation**: Efficiently cache your entirely Go builds.
> - **Smaller Binaries**: Using Cgo generates a C wrapper function for each C function called. Purego doesn't!
> - **Dynamic Linking**: Load symbols at runtime and use it as a plugin system.
> - **Foreign Function Interface**: Call into other languages that are compiled into shared objects.
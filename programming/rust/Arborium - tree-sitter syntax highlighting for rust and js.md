---
created: 2025-12-14T15:15:00.278Z
updated: 2025-12-14T15:15:00.278Z
---
https://arborium.bearcove.eu/#rust

> Finding good [[tree-sitter]] grammars is hard. In arborium, every grammar:

> - Is generated with tree-sitter 0.26
> - Builds for WASM & native via cargo
> - Has working highlight queries
> 
> We hand-picked grammars, added missing highlight queries, and updated them to the latest tree-sitter. Tree-sitter parsers compiled to WASM need libc symbols (especially a C allocator)—we provide [arborium-sysroot](https://github.com/bearcove/arborium/tree/main/crates/arborium-sysroot) which re-exports dlmalloc and other essentials for wasm32-unknown-unknown.

I would love to take a whack at replacing pygments on this site with arborium.

via [bsky](https://bsky.app/profile/fasterthanli.me/post/3m7vw65aadk2p)
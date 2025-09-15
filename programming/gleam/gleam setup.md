---
created: 2025-09-15T12:24:20.299Z
updated: 2025-09-15T12:24:20.299Z
---
```
brew install gleam # to setup a global gleam
mise use gleam # in a project to specify the version
```

Next I tried to configure the LSP in neovim by adding this to my config:
```
vim.lsp.enable('gleam')
```

It seems to be enabled in a gleam buffer, but I don't have syntax highlighting and the LSP doesn't seem to be providing completions or anything.

```
:TSInstall gleam
```

got me syntax highlighting, but the LSP still seems to run and not provide completion or function info. Gonna drop it for now I guess.

## create a project

[docs](https://gleam.run/writing-gleam/)

```
gleam new .
```

Now there's a file in `src/gleam_app.gleam`, and LSP works with it! Seems like the problem was that I was editing a file that wasn't in a gleam "project"
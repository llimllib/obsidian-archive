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

## mess around

Going through the tutorial, I wondered how gleam handled character counts.

```gleam
// these  two are identical, and print 1
io.println(int.to_string(string.length("🇺🇸")))
"🇺🇸" |> string.length |> int.to_string |> io.println

// and there's a built-in grapheme breakdown
io.println(int.to_string(list.length(string.to_graphemes("🇺🇸"))))
```

I was a bit surprised that it uses grapheme length.

- curly braces instead of parens!
- singly-linked lists 😬
- love the `_` placeholder argument
- handy: `If you need to debug print a value in the middle of a pipeline you can use |> echo to do it.`
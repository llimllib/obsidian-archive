---
created: 2024-09-06T19:47:00.235Z
updated: 2024-09-06T19:47:00.235Z
---
https://www.michaelpj.com/blog/2024/09/03/lsp-good-bad-ugly.html

> For a few years now I have been working on the [Haskell Language Server](https://github.com/haskell/haskell-language-server) (HLS), and the [`lsp` library](https://github.com/haskell/lsp) for the LSP protocol and writing LSP servers. Unsurprisingly, I have developed some opinions about the design of the LSP!

A very interesting set of comments on the state of the LSP protocol, which is so central to the modern IDE experience and also... written exclusively by one person at Microsoft:

> The LSP specification has, as far as I can tell, _one_ committer, Dirk Bäumer, who works for Microsoft (I assume on the VSCode team). There have been many small contributions by outsiders, but nobody else has commit access.

> There is zero open discussion of features before they are added to the spec. Typically they are implemented in VSCode, and then the specification is updated as a _fait accompli_ to document those changes

Lots of other good tidbits in there.
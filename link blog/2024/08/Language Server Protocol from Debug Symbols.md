---
created: 2024-08-13T00:13:01.280Z
updated: 2024-08-13T00:13:01.280Z
---
https://www.forrestthewoods.com/blog/language-server-protocol-from-debug-symbols/

> Writing a custom Language Server Protocol implementation for Jai felt like a daunting task. It typically requires parsing the code to figure out what all the symbols and what not are. I don't have the time or energy to do that.

> Then I came up with a crazy and maybe terrible idea. What if instead of trying to parse Jai code I could leverage the debug symbols already produced by the compiler? In theory this should have "perfect" knowledge of symbols and it should work with effectively any compiled language. That seems pretty nifty!

> Well, that's exactly what I did. The end result is a VSCode extension called [fts-lsp-pdb](https://marketplace.visualstudio.com/items?itemName=ForrestTheWoods.fts-lsp-pdb) and it provides `goto definition` support for any language that produces a `pdb` - Jai, C/C++, Zig, etc.

clever idea!
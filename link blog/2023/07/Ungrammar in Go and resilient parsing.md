https://eli.thegreenplace.net/2023/ungrammar-in-go-and-resilient-parsing/

Eli Bendersky wrote a [lexer](https://github.com/eliben/go-ungrammar/blob/a36d6170fb4aecb59142bc57381f7fd190e155e4/lexer.go) and [parser](https://github.com/eliben/go-ungrammar/blob/a36d6170fb4aecb59142bc57381f7fd190e155e4/parser.go) for [ungrammar](https://github.com/rust-analyzer/ungrammar/tree/master) in go.

Ungrammar is a language for specifying concrete syntax trees (trees generated from the source code that still have full information about the source code in detail, and thus have not yet become "abstract syntax trees") which is useful in several ways, but particularly for implementing IDE-like features.

I'm saving this link primarily because it seems like a really good example of how a particularly skilled compiler writer writes a compiler for a simple language.
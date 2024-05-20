---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/softdevteam/grmtools/

Rust grammar tools; allow you to build a parser from a grammar specification. Inclues `lrpar`, which is a `yacc`-compatible parser generator for rust.

Found via [this article on good errors in LR parsers](https://tratt.net/laurie/blog/2020/automatic_syntax_error_recovery.html), which is linked from Laurence Tratt's response to [[Just Write the Parser]]

(It's neat that the way they handle errors in that article is to run a graph search on the grammar, looking for the shortest path to a valid string in the language)
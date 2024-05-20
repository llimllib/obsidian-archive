---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://railsatscale.com//2023-06-12-rewriting-the-ruby-parser/

A team from shopify has rewritten the ruby parser from a bison-generated parser into a hand-written recursive descent parser, and it's going to become the parser for the main ruby interpreter.

The article goes into depth on why they're rewriting it, why they chose to write a hand-written parser, error recovery, and lots of other interesting topics.
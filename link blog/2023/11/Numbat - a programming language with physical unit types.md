---
updated: '2023-11-16T18:48:52Z'
created: '2023-11-16T18:48:52Z'
---
https://numbat.dev/articles/intro.html

> Numbat is a programming language that aims to provide a convenient way to perform computations with physical units. One of the main goals of the language is to help users write correct programs. It has a static type system where physical dimensions act as types. The expression 3 months, for example, has a type of Time. Similarly, the expression 2 years also has a type of Time. The compound expression 3 months + 2 years is therefore well-typed: 

repl: https://numbat.dev/

docs: https://numbat.dev/doc/introduction.html

Very cool. Here's an example repl session showing that if you run 7 min/mi for a marathon, you'll finish in 3 hours and 3 minutes:

```
>>> let marathon = 42.16km
  let marathon: Length = 42.16 kilometre
>>> let pace = 7 min/mi
  let pace: Time / Length = 7 minute / mile
>>> marathon * pace
  marathon × pace
      = 183.379 min    [Time]
```
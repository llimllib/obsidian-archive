---
created: 2024-05-23T17:27:56.928Z
updated: 2024-05-23T17:27:56.928Z
---
https://registerspill.thorstenball.com/p/exploring-the-c4-compiler

> This week I found myself digging through the code of [c4](https://github.com/rswier/c4), an implementation of C “in four functions”, by Robert Swierczek.

> I remember coming across c4 when it was released ten years ago. It got me excited: hey, C in four functions, that means it’s easy to understand right?

> That excitement turned into “oh, I see” as soon as I scrolled through the code. c4 is _dense_, barely commented, and, frankly, strange. It’s unlike anything else I had come across in compiler land...

> That’s not x86 assembly, right? I mean, some of it sounds like x86 — `LEA, ADD —` but then there’s `PSH` and `LEV` and `PRTF`. I’m pretty sure `PRTF` corresponds to our `printf` statement and `PRTF` is _not_ an x86 statement.

> Turns out it’s _bytecode._ This week I figured out that c4 is a bytecode compiler and virtual machine.
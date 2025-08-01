---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/rui314/chibicc

> chibicc is developed as the reference implementation for a book I'm currently writing about the C compiler and the low-level programming. The book covers the vast topic with an incremental approach; in the first chapter, readers will implement a "compiler" that accepts just a single number as a "language", which will then gain one feature at a time in each section of the book until the language that the compiler accepts matches what the C11 spec specifies. I took this incremental approach from [the paper](http://scheme2006.cs.uchicago.edu/11-ghuloum.pdf) by Abdulaziz Ghuloum.

> Each commit of this project corresponds to a section of the book. For this purpose, not only the final state of the project but each commit was carefully written with readability in mind. Readers should be able to learn how a C language feature can be implemented just by reading one or a few commits of this project. For example, this is how [while](https://github.com/rui314/chibicc/commit/773115ab2a9c4b96f804311b95b20e9771f0190a), [array access](https://github.com/rui314/chibicc/commit/75fbd3dd6efde12eac8225d8b5723093836170a5), [?:](https://github.com/rui314/chibicc/commit/1d0e942fd567a35d296d0f10b7693e98b3dd037c), and [thread-local variable](https://github.com/rui314/chibicc/commit/79644e54cc1805e54428cde68b20d6d493b76d34) are implemented. If you have plenty of spare time, it might be fun to read it from the [first commit](https://github.com/rui314/chibicc/commit/0522e2d77e3ab82d3b80a5be8dbbdc8d4180561c).


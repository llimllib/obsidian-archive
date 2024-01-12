https://sillycross.github.io/2023/05/12/2023-05-12/

Good, thorough post that doesn't assume you know exactly what a baseline JIT even is; takes you through what one is and why you would want one before it goes to how they built it.

This is the simplest description of a multi-tier JIT I've read:

> The result of this game is the multi-tier JIT strategy. A _baseline JIT compiler_, which excels at fast compilation but only generates mediocre code, is used to compile functions as soon as they reach a low hotness threshold. Then, for functions that eventually gets really hot, the _optimizing JIT compiler_ kicks in to generate better code for these function at a much higher compilation cost.

From the [previous article](https://sillycross.github.io/2022/11/22/2022-11-22/), very neat approach:

> It is [well-known](https://en.wikipedia.org/wiki/Fundamental_theorem_of_software_engineering) that all problems in computer science can be solved by another level of indirection. In our case, C/C++ is a very good tool to describe the semantics of each bytecode (i.e., what each bytecode should do), but C/C++ is not a good tool to write the most efficient interpreter. So what if we add one level of indirection: we write the bytecode semantical description in C++, _compile it to LLVM IR_, and feed the IR into a special-purpose compiler. The special-purpose compiler will take care of all the dirty work, doing proper transformation to the IR and finally generate a nice tail-call-based interpreter.
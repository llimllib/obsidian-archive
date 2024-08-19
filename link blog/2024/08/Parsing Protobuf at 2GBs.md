---
created: 2024-08-19T11:28:42.216Z
updated: 2024-08-19T11:28:42.216Z
---
https://blog.reverberate.org/2021/04/21/musttail-efficient-interpreters.html

> An exciting feature [just landed in the main branch of the Clang compiler](https://reviews.llvm.org/D99517). Using the `[[clang::musttail]]` or `__attribute__((musttail))` statement attributes, you can now get guaranteed tail calls in C, C++, and Objective-C.

Goes on to describe how mandatory tail calls solve the "an intepreter as a giant switch in a loop is slow" problem I have [[Beating the compiler|referenced]] [[Building the fastest Lua interpreter... automatically|previously]].

> Our design does away with a single big parse function and instead gives each operation its own small function. Each function tail calls the next operation in sequence.
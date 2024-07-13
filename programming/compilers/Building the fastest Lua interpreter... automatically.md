---
updated: 2024-07-13T13:03:59.941Z
created: 2023-10-20T13:54:09Z
---
https://sillycross.github.io/2022/11/22/2022-11-22/

Very cool post about writing a [[luajit]] interpreter in the easiest way - as a giant switch on bytecode ops, generating the LLVM IR, then massaging it into a much faster tail call style automatically.
---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://research.swtch.com/ub

Russ Cox lays out a list of instances where C and C++ could help their users write correct programs, but choose not to.

```c++
#include <stdio.h>

int main() {
    for(int i; i < 10; i++) {
        printf("%d\n", i);
    }
    return 0;
}
```

> If you compile this with clang++ -O1, it deletes the loop entirely: main contains only the return 0. In effect, Clang has noticed the uninitialized variable and chosen not to report the error to the user but instead to pretend i is always initialized above 10, making the loop disappear. 

😱

You need to compile with `-Wall` to get even a warning out of this.

>  Looking over these examples, it could not be more obvious that in modern C and C++, performance is job one and correctness is job two. To a C/C++ compiler, a programmer making a mistake and (gasp!) compiling a program containing a bug is just not a concern. Rather than have the compiler point out the bug or at least compile the code in a clear, understandable, debuggable manner, the approach over and over again is to let the compiler do whatever it likes, in the name of performance. 

> ... One thing I find surprising, though, is that correctness gets ignored even when it clearly doesn’t hurt performance. It would certainly not hurt performance to emit a compiler warning about deleting the if statement testing for signed overflow, or about optimizing away the possible null pointer dereference in Do(). Yet I could find no way to make compilers report either one; certainly not -Wall. 

He closes with a lovely quote from [John Regehr](https://blog.regehr.org/archives/226):

>    It is basically evil to make certain program actions wrong, but to not give developers any way to tell whether or not their code performs these actions and, if so, where. One of C’s design points was “trust the programmer.” This is fine, but there’s trust and then there’s trust. I mean, I trust my 5 year old but I still don’t let him cross a busy street by himself. Creating a large piece of safety-critical or security-critical code in C or C++ is the programming equivalent of crossing an 8-lane freeway blindfolded.
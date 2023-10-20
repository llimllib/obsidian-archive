https://felixk15.github.io/posts/c_ocoa/
https://github.com/FelixK15/c_ocoa

> The overall plan is to have a C API which, under the hood, uses the ObjC runtime to call functions that are normally only accessible when programming in ObjC.

> The first step is to query metadata about the class that we’re interested in turning into a C API. The code generator works by providing it with one or more ObjC class name(s) (optionally including wildcards). For each class the generator generates a pair of .c/.h files.

> ObjC is an object oriented language, C is not. So we need some way to map ObjC’s “object orientness” to C functions... For this problem I decided to flatten the class hierarchy of the class that you want to export to C... Unlike C++, ObjC does not support multiple inheritance (thank god!), so this process is rather straight-forward.


---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://tiarkrompf.github.io/notes/?/just-write-the-parser/

> This is a whirlwind tour of writing parsers by hand. Why would you want to do that, when tools like Yacc exist to do it for you?

----

[aside 1](https://tiarkrompf.github.io/notes/?/just-write-the-parser/aside1) got a fair amount of attention for:

> The theory of formal languages and their relation to automata, logic, and complexity is beautiful. But if the goal is to convey practical compiler-building skills I believe we should forget about most of the formalisms focused on subclasses of context-free languages and instead teach students straightforward methods to write parsers by hand

Including [this response](https://tratt.net/laurie/blog/2023/why_we_need_to_know_lr_and_recursive_descent_parsing_techniques.html) from Laurence Tratt (Royal Academy of Engineering Research Chair in Language Engineering):

>  I have had the dubious pleasure of converting a number of recursive descent parsers to LR grammars and none of the non-trivial recursive descent parsers has parsed the language their authors expected. Sometimes they accept inputs they shouldn't; sometimes they reject inputs they shouldn't.

...

> There are two other use-cases for recursive descent parsing. The first is performance. Although there aren't, to the best of my knowledge, modern performance numbers, it is reasonable to assume that recursive descent parsing is generally faster than LR parsing. However, "faster" is relative: on modern machines, even a naive LR parser on a huge grammar will happily parse thousands of lines of code a second which is enough for the vast majority of use cases. The second is error recovery. LR parsers have traditionally had terrible error recovery. Immodestly, I now claim that [some work I was involved in](https://tratt.net/laurie/blog/2020/automatic_syntax_error_recovery.html) allows LR parsers to have error recovery that is better than all but the best recursive descent parsers.


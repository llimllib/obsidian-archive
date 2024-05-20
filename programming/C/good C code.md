---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
What makes good C code?

Here's some that I consider good: https://github.com/Tarsnap/tarsnap/blob/3d85cc1f27b5319c7e175fea2b89290a1bd7905a/lib/keyfile/keyfile.c

Note the focus on clarity, simplicity, and on cleaning everything up.

> One thing most people overlook: Experienced C developers often don't use it as a low-level language. Rather, they use libraries which extend the language with higher level constructs.
> https://twitter.com/cperciva/status/1508293710139731968

> C doesn't have linked lists as a native data type. But include the right header and you'll have macros for declaring a linked list and inserting/removing/traversing. Same goes for "elastic" (automatically re-allocating as needed) arrays. Not in C, but with the right header...
> https://twitter.com/cperciva/status/1508319637032767490?s=20&t=gFZzPVNBOlp4ArXpmxfxng

Which is in response to a Dan Luu thread: https://twitter.com/elazarl/status/1508343105828892679

The security counter-argument is:

> In my neck of the woods, people get flak for using C/C++ because of the security externalities, not because of some scorn for the effectiveness of the tool. There is no proof that anyone is effective at writing secure code in C/C++. It's not the wrong brush, it's lead paint.
> https://twitter.com/FiloSottile/status/1508419644553674754
> - Filippo Valsorda


---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
Wonderful article, with really nice interactive breakdowns of how golang calls functions at the ASM level: https://planetscale.com/blog/generics-can-make-your-go-code-slower

> It looks quite familiar, but there’s a stark difference. Offset `0x0094` contains what we don’t want a function call-site to contain: _another_ pointer dereference. The technical term for this is, again, a total bummer.

Even makes `monomorphization` seem like a nice simple term!
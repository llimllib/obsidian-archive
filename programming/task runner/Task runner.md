---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
I usually use makefiles.

[[just]] is interesting, it takes makefile syntax(ish) and has better errors and helpful command output. Supports dependencies between jobs

[Taskfile](https://github.com/adriancooney/Taskfile) is pretty great too, replaces a makefile with a dead simple set of shell scripts. Includes a template to get you started, but really is just bash.

[mask](https://github.com/jacobdeichert/mask) takes an interesting approach by requiring you to define your tasks in a markdown file
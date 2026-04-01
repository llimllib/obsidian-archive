---
created: 2026-04-01T18:02:17.942Z
updated: 2026-04-01T18:02:17.942Z
---
For taking a screenshot with zsh, I launch it with:

`env -i TERM=$TERM TERMINFO=$TERMINFO HOME=$HOME PS1="$ " PATH=$PATH zsh -f`

- use the same `$HOME`, `$PATH`, `$TERM` and `$TERMINFO`
- use a very simple `PS1`
- launch without loading the config file
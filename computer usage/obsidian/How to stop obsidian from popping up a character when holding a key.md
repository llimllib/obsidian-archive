---
created: 2026-01-29T21:41:57.530Z
updated: 2026-01-29T21:41:57.530Z
---
If you're in vim mode, and you hold `l` to move to the right, mac OS X pops up a character selection box that is annoying, useless, and distracting in this context (but might be useful elsewhere)

To prevent this, set a default:

```
defaults write md.obsidian ApplePressAndHoldEnabled -bool false
```

If you would rather prevent it system-wide:

```
defaults write -g ApplePressAndHoldEnabled -bool false
```

Solution via [this thread](https://forum.obsidian.md/t/vim-enable-key-repeat-option/1095/3)
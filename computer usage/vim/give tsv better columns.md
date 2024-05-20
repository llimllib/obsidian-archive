---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
`%!column -t -s $'\t'`

This will create a table (`-t`) from columns spearated by tab characters (`-s $'\t'`)
- by default, it will split on any whitespace, so you can use -s to tell it what to split by
- `$'\t'` is a cute bash-ism to represent a single tab character using [[bash ANSI quoting]]
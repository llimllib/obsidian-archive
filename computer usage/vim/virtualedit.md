---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
To edit anywhere in a buffer, whether there are characters there or not, `set ve=all`. Doesn't let you go past the end of the buffer, so you might have to add some lines.

Saw it while looking at [this ascii drawing plugin](https://github.com/jbyuki/venn.nvim)

`ve` is short for `virtualedit`; [docs here](http://vimdoc.sourceforge.net/htmldoc/options.html#'virtualedit')
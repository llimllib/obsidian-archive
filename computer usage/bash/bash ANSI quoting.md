Bash strings quoted with `$'<text here>'` allow literal escapes to appear in the text.

So, `$'\t'` represents a one-character literal tab character, while '\t' is two characters, a slash followed by a t.

[documentation here](https://www.gnu.org/software/bash/manual/html_node/ANSI_002dC-Quoting.html#ANSI_002dC-Quoting), including a full list of available escapes
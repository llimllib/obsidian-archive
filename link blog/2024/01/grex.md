---
updated: '2024-01-19T02:39:59Z'
created: '2024-01-19T02:39:59Z'
---
https://github.com/pemistahl/grex

Neat tool, you give it a few examples of strings you'd like to match and it generates and shows you a regex that matches them, with several different options for how to generate the regex.

A simple example:

```
$ grex -r b ba baa baaa
^b(?:a{1,3})?$
```
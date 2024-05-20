---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
To print out the value of a variable, use the `info` command

```make
GOFILES=$(shell find . -iname '*.go')
$(info [$(GOFILES)])
```

in this example, we've added literal `[]` around the value of the variable to make the output clearer.

[docs](https://www.gnu.org/software/make/manual/html_node/Make-Control-Functions.html)
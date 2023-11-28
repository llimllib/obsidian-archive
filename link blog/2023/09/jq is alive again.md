https://github.com/jqlang/jq/releases/tag/jq-1.7

> After a five year hiatus we're back with a GitHub organization, with new admins and new maintainers who have brought a great deal of energy to make a long-awaited and long-needed new release. 

[[jq]] is alive again! I am excited to see what the new maintainers bring to the table.

`pick` looks pretty neat:

```shell
$ jq -n '{"a": 1, "b": {"c": 2, "d": 3}, "e": 4} | pick(.a, .b.c, .x)'
{
  "a": 1,
  "b": {
    "c": 2
  },
  "x": null
}
```
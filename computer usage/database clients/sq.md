---
created: 2024-08-19T01:40:25.595Z
updated: 2024-08-19T01:40:25.595Z
---
https://sq.io/

`sq` is a free/libre [open-source](https://github.com/neilotoole/sq) data wrangling swiss-army knife to inspect, query, join, import, and export data. You could think of `sq` as [jq](https://jqlang.github.io/jq/) for databases and documents, facilitating one-liners like:

```shell
sq '@postgres_db | .actor | .first_name, .last_name | .[0:5]'
```

Looks like a very neat tool for querying databases in a jq style, I've not tried it yet
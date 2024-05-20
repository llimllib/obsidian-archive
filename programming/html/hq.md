---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/orf/hq

> `hq` reads HTML and converts it into a JSON object based on a series of CSS selectors. The selectors are expressed in a similar way to JSON, but where the values are CSS selectors. For example:

```
{posts: .athing | [ {title: .titleline > a, url: .titleline > a | @(href)} ] }
```

jq, but for HTML. Similar to [[pup]] but maybe more maintained?
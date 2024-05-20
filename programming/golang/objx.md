---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/stretchr/objx

Objx provides the `objx.Map` type, which is a `map[string]interface{}` that exposes a powerful `Get` method (among others) that allows you to easily and quickly get access to data within the map, without having to worry too much about type assertions, missing data, default values etc.

Objx uses a predictable pattern to make access data from within `map[string]interface{}` easy. Call one of the `objx.` functions to create your `objx.Map` to get going:

```
m, err := objx.FromJSON(json)
```
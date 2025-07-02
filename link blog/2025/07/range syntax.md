---
created: 2025-07-02T11:36:43.778Z
updated: 2025-07-02T11:36:43.778Z
---
Love this idea for range syntax [from Tony Finch](https://dotat.at/@/2025-07-02-cmp.html)

> I’m also dissatisfied with the range or slice syntax in basically every programming language I’ve seen. I thought it might be nice if the cute comparison and iteration syntaxes were aspects of a more generally useful range syntax, but I couldn’t make it work.

> Until recently when I realised I could make use of prefix or mixfix syntax, instead of confining myself to infix.

> So now my fantasy pet range syntax looks like

```
    >= min < max    // half-open
    >= min <= max   // inclusive
```

> And you might use it in a [pattern match](https://dotat.at/@/2025-05-13-if-is.html)

```
    if x is >= min < max {
        // ...
    }
```

> Or as an iterator

```
    for x in >= min < max {
        // ...
    }
```

> Or to take a slice

```
    xs[>= min < max]
```
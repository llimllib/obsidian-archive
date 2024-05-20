---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/jetpack-io/typeid

> TypeIDs are a modern, type-safe extension of UUIDv7.

> TypeIDs are canonically encoded as lowercase strings consisting of three parts:

> 1. A type prefix
> 2. An underscore '_' separator
> 3. A 128-bit UUIDv7 encoded as a 26-character string in base32 (using [Crockford's alphabet](https://www.crockford.com/base32.html) in lowercase).

> Here's an example of a TypeID of type `user`:

```
  user_2x4y6z8a0b1c2d3e4f5g6h7j8k
  └──┘ └────────────────────────┘
  type    uuid suffix (base32)
```

Interesting idea to include the type as part of the UUID canonically. Has very similar properties to ULIDs or UUIDv7, but the type prefix is the main selling point. (Also that they specify encoding with base32, unlike the usual representation of UUIDs)
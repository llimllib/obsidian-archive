---
created: 2024-07-17T17:18:10.078Z
updated: 2024-07-17T17:18:10.078Z
---
https://cedardb.com/blog/german_strings/

An article about a particular method ("German strings") for representing strings in databases.

- For short (<12 byte) strings, it's a 4 byte length followed by 12 bytes, avoiding the need for a pointer dereference
```
 0                   1                   2                   3  
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                             length                            |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                                                               |
+                                                               +
|                             string                            |
+                                                               +
|                                                               |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

- For anything else, it's a 4 byte length, followed by 4 bytes of its prefix, 2 bits of "class", and 62 bits of pointer
```
 0                   1                   2                   3  
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                             length                            |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|                             prefix                            |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
|cl.|                                                           |
+-+-+                                                           +
|                            pointer                            |
+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

They hint at, but don't talk about, the encoding of the string. I assume that they're utf-8 encoding the string into bytes, but don't say, for example, how they treat a long string which changes meaning or becomes invalid if you chop off the 13th byte. (For example, imagine the 11th and 12th bytes are a [combining diaeresis](https://codepoints.net/U+0308?lang=en) or a 4-byte emoji spans the 12th byte)

They point to [[duckdb]]'s [string implementation](https://github.com/duckdb/duckdb/blob/main/src/include/duckdb/common/types/string_type.hpp) as an example; as far as I can tell from a quick scan it doesn't use the two-bit class, but instead just a regular 64-bit pointer.

They also point to [apache arrow](https://arrow.apache.org/docs/format/Columnar.html#variable-size-binary-view-layout) and [polars](https://pola.rs/posts/polars-string-type/) documentation of their string types.
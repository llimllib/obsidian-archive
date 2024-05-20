---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://sqlite.org/json1.html#json5

via the [release notes](https://sqlite.org/releaselog/3_42_0.html) for 3.42.

Worth noting that they seem to support json5 input, but not output; so I assume any comments or other non-standard json in your json5 document will be stripped if it round trips through the database.
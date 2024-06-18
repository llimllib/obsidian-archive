---
created: 2024-06-18T17:03:31.169Z
updated: 2024-06-18T17:03:31.169Z
---
[[vitest]] (which is otherwise quite good) clobbers stderr, and its developers [do not seem to understand how stderr works](https://github.com/vitest-dev/vitest/issues/2671#issuecomment-1568859480) so it's not considered a problem.

This can cause problems in development where your code is writing errors out to stderr, but vitest is hiding them from you.

If you want to see stderr output, the best you can do is use the `dot` reporter, which unfortunately can still overwrite your stream, or `tap` which will buffer all output but doesn't seem to overwrite your output.

`vitest run test/something.ts --reporter=dot`

Alternately, you can force everything to use stdout, but that can be quite painful.
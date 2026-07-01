---
created: 2026-06-30T13:23:37.073Z
updated: 2026-06-30T13:23:37.073Z
---
https://cekrem.github.io/posts/parse-dont-validate-typescript/

A practical exercise walking through how to "[[Parse, don't validate]]" in plain typescript. I did not know about the "brand" technique, so that was neat to learn.

I generally like to do a light version of this, but I also often find it frustrating and brittle when people go down the FP-style "All Information Must Be Encoded in the Type System" rabbit hole.

When it comes down to it, I'm a caveman who prefers to bash rocks instead of teach math

(One note: I suffered terribly at one job that had extensive Zod types with the slow compilation time they caused. "Parse, don't validate" isn't free, and shouldn't be treated as such. This does not mean you should not use it, just that one needs to properly weigh the costs, and that it can often be difficult to do so ahead of time)
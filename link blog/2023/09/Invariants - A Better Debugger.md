---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://brooker.co.za/blog/2023/07/28/ds-testing.html

> I spent days banging my head on the problem with printfs and debuggers and just wasn't making progress. The TA was no help. I asked a CS graduate student I knew that lived nearby, and his approach just blew my mind.

> He sat me down with a piece of paper, and went through the algorithm step-by-step, asking _what is true about the data structure at this step?_after each one. Together, we came up with a set of step-by-step invariants, and some global invariants that must hold true after every run of the algorithm. Within minutes of getting back to my desk and writing the tests for the invariants, I had found my bug: a `>` which should have been `>=`.

——

> Some of these invariants are rather expensive to test for, such as the last one which requires _O(N log N)_ work. They aren't always practical to assert on each step in a production implementation, but are very practical to test for in a set of unit tests. My experience has been that reasoning about, listing, and then testing for invariants like this is a much better way to test data structures like this than testing through the interfaces.

Via [tqbf](https://infosec.exchange/@tqbf/110995587250475638) on mastodon 
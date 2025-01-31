---
created: 2025-01-31T15:26:36.195Z
updated: 2025-01-31T15:26:36.195Z
---
A new audio programming language from the author of [supercollider](https://supercollider.github.io/), with a very nice manifesto in the README:

> APL and FORTH (from which Joy derives) are both widely derided for being write-only languages. Nevertheless, there has yet to be a language of such concise expressive power as APL or its descendants. APL is powerful not because of its bizarre symbols or syntax, but due to the way it automatically maps operations over arrays and allows iterations at depth within arrays. This means one almost never needs to write a loop or think about operations one-at-a-time. Instead one can think about operations on whole structures.

...

> There are several reasons I like the concatenative style of programming:
    Function composition is concatenation. 
    Pipelining values through functions to get new values is the most natural idiom.
    Functions are applied from left to right instead of inside out.
> 

Some examples of the language:

```
;; play a sine wave at 800 Hz and initial phase of zero.
800 0 sinosc .3 * play   

;; the analog bubbles example from SuperCollider:
.4 0 lfsaw 2 * [8 7.23] 0 lfsaw .25 * 5/3 + + ohz 0 sinosc .04 * .2 0 4 combn play
```

more [here](https://github.com/lfnoise/sapf/blob/main/sapf-examples.txt)

via [toot](https://sonomu.club/@madskjeldgaard/113921744905363935)
---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://mcilloni.ovh/2023/07/23/unicode-is-hard/

A nice walk through the history of unicode, along with code samples in python and C, explaining why each encoding sucks (but UTF-8 sucks the least) and unicode is not easy.

> The beauty of UTF-8 is that code that splits, searches or synchronises using ASCII _symbols_[8](https://mcilloni.ovh/2023/07/23/unicode-is-hard/#fn:10) will work fine as-is, with little to no modification, even with Unicode text.

---

> Another headache is the fact Unicode also may define special forms for the same letter or group of letters, which are visibly different but understood by humans to be derived from the same symbol.

> A very common example of this is the `ﬁ` (U+FB01), `ﬂ` (U+FB02), `ﬀ` (U+FB00) and `ﬃ` (U+FB03) ligatures, which are ubiquitous in Latin text as a “more readable” form of the `fi`, `fl` and `ffi` digraphs. In general, users expect `office`, `ofﬁce` and `oﬃce` to be treated and rendered similarly, because they all represent the same identical word, but not necessarily without any visual difference. [9](https://mcilloni.ovh/2023/07/23/unicode-is-hard/#fn:11)

----

There is a section on the different types of unicode normalizations, which is very helpful for me as I always get them confused
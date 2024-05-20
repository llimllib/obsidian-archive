---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://web.dev/articles/base64-encoding

Encoding unicode strings to base64 in javascript is not easy, but it is possible.

I knew that Javascript used UTF-16 internally, but today I learned about:
- [String.fromCodePoint()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/fromCodePoint) - convert a sequence of code points into a string
- [TextEncoder](https://developer.mozilla.org/en-US/docs/Web/API/TextEncoder) - allows you to convert a sequence of code points into a UTF-8 byte sequence
- [TextDecoder](https://developer.mozilla.org/en-US/docs/Web/API/TextDecoder) - convert a byte sequence to a stream of code points from a variety of text encodings
- [String.isWellFormed()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/isWellFormed) - a new-ish function to check whether a string has any lone surrogates (is invalid UTF-16 - see [[wtf-8]])
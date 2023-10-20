https://simonsapin.github.io/wtf-8/#motivation

> Unpaired surrogate 16-bit code units are the only case where an arbitrary sequence of 16-bit code units is ill-formed in UTF-16. UTF-8, however, is more complex and maintaining its well-formedness is arguably more valuable.

> This specification defines WTF-8, a superset of UTF-8 that can losslessly represent arbitrary sequences of 16-bit code unit (even if ill-formed in UTF-16) but preserves the other well-formedness constraints of UTF-8.
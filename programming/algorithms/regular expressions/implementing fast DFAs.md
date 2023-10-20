this gist from Per Vognsen: https://gist.github.com/pervognsen/218ea17743e1442e59bb60d29b1aa725

demonstrates how to speed up a naive DFA table implementation. Is a bit over my head, but interesting.

It's used in postgres here: https://github.com/postgres/postgres/blob/f45f8b7ff3fe6c8b8139e177bb3fec7629ef9f05/src/common/wchar.c#L1754

and re2 here: https://github.com/google/re2/blob/0eeb044607f3d99e623941939fa7c527a97a7113/re2/prog.cc#L978
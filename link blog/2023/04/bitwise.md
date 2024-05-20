---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/mellowcandle/bitwise

command-line byte calculator

```
$ bitwise 0x123123d
Unsigned decimal: 19075645
Signed decimal: 19075645
Hexadecimal: 0x123123d
Octal: 0110611075
Human: 18.19 MiB
Radix64: x6l6/
IPv4 (Network byte order - Big):  61.18.35.1
IPv4 (Reverwsed byte order - Little):  1.35.18.61
ASCII: .....#.=
Binary:
0 0 0 0 0 0 0 1 | 0 0 1 0 0 0 1 1 | 0 0 0 1 0 0 1 0 | 0 0 1 1 1 1 0 1
    31 - 24           23 - 16           15 -  8            7 -  0
```

Can do math as well:

```
$ bitwise "0x30 * 0x20 / 2"
Unsigned decimal: 768
Signed decimal: 768
Hexadecimal: 0x300
Octal: 01400
Human: 768
Radix64: .A
IPv4 (Network byte order - Big):  0.3.0.0
IPv4 (Reverwsed byte order - Little):  0.0.3.0
ASCII: ........
Binary:
0 0 0 0 0 0 1 1 | 0 0 0 0 0 0 0 0
    15 -  8            7 -  0
```

Very cool!

From [this toot](https://types.pl/@lenary/110141999448828497)
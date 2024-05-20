---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/wader/fq

> Tool, language and decoders for working with binary data...

> In summary it aims to be jq, hexdump, dd and gdb for files combined into one.

intends to be like `jq` but for binary files. Note that the `fq` in homebrew is not the correct one - `brew install wader/tap/fq` to install.

```console
$ fq . Screenshot\ 2023-03-29\ at\ 4.06.41\ PM.png
       |00 01 02 03 04 05 06 07|01234567|.{}: Screenshot 2023-03-29 at 4.06.41 PM.png (png)
0x00000|89 50 4e 47 0d 0a 1a 0a|.PNG....|  signature: raw bits (valid)
0x00008|00 00 00 0d 49 48 44 52|....IHDR|  chunks[0:47]:
*      |until 0x9a0d9.7 (end) (|        |
```


---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
I didn't know what `-fPIC` meant in gcc invocations; I was seeing it when messing around with sqlite extension compilation. [this SO response](https://stackoverflow.com/a/5311538/42559) is helpful:

> Position Independent Code means that the generated machine code is not dependent on being located at a specific address in order to work.

> E.g. jumps would be generated as relative rather than absolute.

> Pseudo-assembly:

> PIC: This would work whether the code was at address 100 or 1000

```makefile
100: COMPARE REG1, REG2
101: JUMP_IF_EQUAL CURRENT+10
...
111: NOP
```

> Non-PIC: This will only work if the code is at address 100

```makefile
100: COMPARE REG1, REG2
101: JUMP_IF_EQUAL 111
...
111: NOP
```
```
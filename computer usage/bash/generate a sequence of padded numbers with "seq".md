---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
```
$ seq -f "%02g" 1 10
01
02
03
04
05
06
07
08
09
10
```

Then, say you want to create a directory with each of those numbers:

```
for i in $(seq -f "%02g" 1 25); do mkdir "$i"; done
```

`-f` means "use a printf style format to print each number"

I had to go read the printf manual to find out what `g` means, but I still mostly don't understand:

```
gG          The argument is printed in style f (F) or in style e (E) whichever gives full precision in minimum space.
```

`%02d` doesn't work, I guess because the `seq` manual states `All numbers are interpreted as floating point.`
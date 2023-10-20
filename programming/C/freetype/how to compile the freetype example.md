[here](https://freetype.org/freetype2/docs/tutorial/step1.html) is the freetype tutorial, which includes a link (hidden at the end(!?)) to [an example C program](https://freetype.org/freetype2/docs/tutorial/example1.c) with limited instructions for how to use the thing.

This makefile builds it, which it took me a bit to figure out:

```make
INCLUDE_FLAGS=$(shell pkg-config --cflags --libs freetype2)

example: example1.c
	$(CC) $(INCLUDE_FLAGS) $< -o $@
```

- the tutorial gives `pkg-config --cflags freetype2`, but it took me some googling to figure out `--cflags --libs` was what I wanted - this outputs three types of flags:
	- `-I` tells the c compiler where to find the header files
	- `-L` tells the c compiler where to find the dynamic library for freetype
	- `-l` tells the c compiler what library to choose, maybe?
	- The full output on this system is: `-I/opt/homebrew/opt/freetype/include/freetype2 -L/opt/homebrew/opt/freetype/lib -lfreetype`
	- I had tried combinations of `-I`, and one of `-L` and `-l` before finding that you needed all three, for reasons that are not clear to me
- `$<` means "all prerequisites of this task" which in this case is just `example1.c`
- `$@` means "the output file of this task" which in this case is `example`
- I was able to run the example program and it prints something giant to my console that I don't understand


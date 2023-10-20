https://nullprogram.com/blog/2022/05/22/

Nice explanation of how the author built a (windows-only) program to process a file tree and display the number of lines of source code in each directory.

It's an exercise in over-optimization, but intentionally. Also parallelizes the tree building, which is nice.

Full source [here](https://github.com/skeeto/scratch/blob/5129fd45153999924334c5a989216e98cb5e1098/misc/watc.c)

(I'd love to replicate this in zig for kicks)
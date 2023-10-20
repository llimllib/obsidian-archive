https://dougallj.wordpress.com/2022/08/20/faster-zlib-deflate-decompression-on-the-apple-m1-and-x86/

> Most of the speedup just comes from reading and applying Fabian Giesen’s posts ([[intro to dataflow graphs]]) on Huffman decoding

> The goal was to use roughly the following [variant-4-style](https://fgiesen.wordpress.com/2018/02/20/reading-bits-in-far-too-many-ways-part-2/#:~:text=Variant%204%3A%20a%20different%20kind%20of%20lookahead) loop to decode and unconditionally refill with eight-cycle latency on Apple M1...

Very detailed analysis of how to speed up deflate (and urging you to use zstd instead)
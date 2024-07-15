---
updated: '2023-12-15T20:40:19Z'
created: '2023-10-20T13:54:09Z'
---
## Common cryptographic hash functions:

- legacy algorithms:
	- [md4](https://en.wikipedia.org/wiki/MD4)
	- [md5](https://en.wikipedia.org/wiki/MD5)
	- [sha-1](https://en.wikipedia.org/wiki/SHA-1)
- current algorithms:
	- [sha-2](https://en.wikipedia.org/wiki/SHA-2)
	- [sha-3](https://en.wikipedia.org/wiki/SHA-3)

## Common non-cryptographic hash functions:
These hash functions are faster than cryptographic hash functions, but less secure, which can be useful for applications such as [[programming/algorithms/bloom filters]]:

- [xxhash](https://github.com/Cyan4973/xxHash)
	- has several versions and a handy [benchmarks table](https://github.com/Cyan4973/xxHash#benchmarks) vs other hashes
- [murmur3](https://github.com/rurban/smhasher/blob/master/MurmurHash3.cpp)
	- hosted as part of the handy [smhasher tool](https://github.com/rurban/smhasher) which includes a [website with a table](https://rurban.github.io/smhasher/) of many more hashes than I will list here, and information on their performance and quality
- [jenkins](https://en.wikipedia.org/wiki/Jenkins_hash_function)
- [fxhash](https://nnethercote.github.io/2021/12/08/a-brutally-effective-hash-function-in-rust.html)
	- developed for use in firefox, and implemented [implemented in](https://docs.rs/fxhash/latest/fxhash/struct.FxHasher.html) [[Rust]]
- [city hash](https://github.com/google/cityhash), which comes out of work done at google
- [fnv hash](http://www.isthe.com/chongo/tech/comp/fnv/), a series of fast hash functions
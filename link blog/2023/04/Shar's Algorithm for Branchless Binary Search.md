---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://probablydance.com/2023/04/27/beautiful-branchless-binary-search/

The author finds Shar's Algorithm from binary search, which is from TAOCP, and implements it in C++. Finds that it is sometimes faster than the standard library binary search, and does an excellent job benchmarking and explaining why it is or isn't in given scenarios.

> This is the [second time](https://probablydance.com/2018/06/16/fibonacci-hashing-the-optimization-that-the-world-forgot-or-a-better-alternative-to-integer-modulo/) that I came across an algorithm in Knuth’s books that is brilliant and should be used more widely but somehow was forgotten. Maybe I should actually read the book… It’s just really hard to see which ideas are good and which ones aren’t. For example immediately after sketching out Shar’s algorithm, Knuth spends far more time going over a binary search based on the Fibonacci sequence. It’s faster if you can’t quickly divide integers by 2, and instead only have addition and subtraction. So it’s probably useless, but who knows? When reading Knuth’s book, you have to assume that most algorithms are useless, and that the good things have been highlighted by someone already. Luckily for people like me, there seem to still be a few hidden gems.
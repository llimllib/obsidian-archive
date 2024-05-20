---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://www.quantamagazine.org/sci-fi-writer-greg-egan-and-anonymous-math-whiz-advance-permutation-problem-20181105/

Neat article about finding bounds for "superpermutation", which is a sequence that contains every possible permutation of a collection of symbols.

For example, the numbers `1,2,3` have six possible permutations: `123, 132, 213, 231, 312 321`; if you order them in a sequence you get eighteen symbols: `123132213231312321`. But then you can observe that if you order them differently, you can reduce that to a sequence of 15 symbols, which contains all six possible permutations: `123121321`.

For n <= 5, the number of superpermutations is a simple equation: `n! + (n-1)! + ...  + 1`. However, in 2014, it was discovered that this surprisingly isn't true for `n = 6`!

Then a 4chan poster (!) , a science fiction author, and some mathematicians put bounds around the possible values of superpermutations by making an isomorphism to the traveling salesman problem. 

Finding superpermutations is equivalent to the asymmetric (different costs in different directions of travel) traveling salesman problem in a simple way: the cost to visit another city is the number of digits you have to add to the sequence. So `cost(123, 231)` is `1`, `cost(123, 321)` is `2`, and so forth.
https://sillycross.github.io/2023/05/12/2023-05-12/

Good, thorough post that doesn't assume you know exactly what a baseline JIT even is; takes you through what one is and why you would want one before it goes to how they built it.

This is the simplest description of a multi-tier JIT I've read:

> The result of this game is the multi-tier JIT strategy. A _baseline JIT compiler_, which excels at fast compilation but only generates mediocre code, is used to compile functions as soon as they reach a low hotness threshold. Then, for functions that eventually gets really hot, the _optimizing JIT compiler_ kicks in to generate better code for these function at a much higher compilation cost.


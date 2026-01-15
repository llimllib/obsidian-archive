---
created: 2025-10-17T01:41:01.643Z
updated: 2025-10-17T01:41:01.643Z
---
> A “quine” is a deterministic program that prints itself. In this essay, I will show you a “gauguine”: a probabilistic program that infers itself. A gauguine is repeatedly asked to guess its own source code. Initially, its chances of guessing correctly are of course minuscule. But as the gauguine observes more and more of its own previous guesses, it detects patterns of behavior and gains information about its inner workings. This information allows it to bootstrap self-knowledge, and ultimately discover its own source code. We will discuss how—and why—we might write a gauguine, and what we stand to learn by constructing one.

- [Chandra et al](https://dl.acm.org/doi/pdf/10.1145/3759429.3762631) in "Gauguin, Descartes, Bayes: A Diurnal Golem’s Brain"

Contains a lovely quote I'd not read before from [George Pugh](https://archive.org/details/biologicalorigin0000pugh/page/154/mode/2up?q=%22if+the+human+brain%22):

> If the human brain were so simple that we could understand it, then we would be so simple that we couldn’t

The racket source code for his (for surely Chandra is the author of this article?) "gaugine" is [here in racket](https://github.com/kach/gauguine/blob/0ee1178f79ba58b72724035bdd1481d06b1dca8e/gauguine.rkt), only 122 lines

via [bsky](https://bsky.app/profile/cscheid.net/post/3m35slxsqr22l)
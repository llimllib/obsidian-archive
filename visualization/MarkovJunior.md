https://github.com/mxgmn/MarkovJunior

> MarkovJunior is a probabilistic programming language where programs are combinations of rewrite rules and inference is performed via constraint propagation. MarkovJunior is named after mathematician [Andrey Andreyevich Markov](https://en.wikipedia.org/wiki/Andrey_Markov,_Jr.), who defined and studied what is now called [Markov algorithms](https://en.wikipedia.org/wiki/Markov_algorithm).
> In its basic form, a MarkovJunior program is an ordered list of rewrite rules. For example, [MazeBacktracker](https://github.com/mxgmn/MarkovJunior/blob/main/models/MazeBacktracker.xml) (animation on the left below) is a list of 2 rewrite rules:

> 1.  `RBB=GGR` or "replace red-black-black with green-green-red".
> 2.  `RGG=WWR` or "replace red-green-green with white-white-red".

Very cool interactive examples; I don't understand it completely, but it helps in gaining a feel for the system at the very least.
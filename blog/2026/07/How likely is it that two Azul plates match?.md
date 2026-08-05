---
created: 2026-07-31T16:01:59.521Z
updated: 2026-07-31T16:01:59.521Z
draft: true
---
At the start of a round in the game called [Azul](https://en.wikipedia.org/wiki/Azul_(board_game)), there are 9 "plates" each of which contain 4 tiles with one of 5 patterns on them. Wiki has a photo of the game in play:
![[Pasted image 20260731120333 1.png]]

This weekend my friend noticed that many rounds featured plates with the same four tiles on them, and wondered how likely it is, which gave me a fun quick combinatorics problem to solve. 

This problem is very similar to the [birthday problem](https://en.wikipedia.org/wiki/Birthday_problem), with the exception that we have to figure out the number of possible plates.

Since I haven't solved a problem like it in a while, here's how I came up with a back-of-the-napkin estimate, and then (for this article) found the correct answer.

**Idea: We can approximate it as the _number of possible plates_ divided by the _number of comparisons_**

# The napkin answer
## number of comparisons

The number of comparisons is pretty easy, there are 9 plates and we want to know every way to compare them against one other. Honestly I just drew it out and counted, because it's been too long for me to remember this stuff off hand, but we can use the [binomial coefficient](https://en.wikipedia.org/wiki/Binomial_coefficient) to get $(9*8)/2 = 36$ is 9 choose 2, often denoted $\binom{9}{2}$ . Working it out fully:

$$\binom{9}{2} = \dfrac{9!}{2! * (9 - 2)!} = \dfrac{9!}{2*7!} = \dfrac{9*8}{2} = 36$$
## number of possible plates

The number of possible plates is a bit more tricky, but not too bad. Since the tiles are drawn from a bag, they are drawn without replacement and we would have to consider that one type of tile is less likely to be drawn again after it's drawn once, but we can take a simplifying assumption that they're equally likely to be drawn from the bag, and assume that it's going to give us a good enough™ answer for our game night crowd.

To count the number of plates, we need to keep in mind that the order the tiles are drawn does not matter - {<span style="color:blue">blue</span>, <span style="color:red">red</span>} is the same to us as {<span style="color:red">red</span>, <span style="color:blue">blue</span>}.

Since this took me a minute to figure out (I don't do enough math these days!), let's figure this three different ways.

In the following, we'll call the five different tiles {r, b, g, p, o}
### piecewise

Instead of taking it in big chunks, let's divide the ways the plate could be split into 5 groups:

- all one color: there are **5** sets: $\{r,r,r,r\},\ldots\{o,o,o,o\}$
- **3+1**: there are **20** sets: $\{r,r,r,b\},\ldots\{o,o,o,p\}$
	- for each of the first sets, replace the final color with each of the other 4 colors
- **2+2**: there are **10** sets: $\{r,r,b,b\}\ldots\{o,o,p,p\}$
	- same as the last one, but $\{r,r,b,b\} = \{b,b,r,r\}$ so there's half as many
- **2+1+1**: there are **30** sets: $\{r,r,b,g\},\ldots\{o,o,p,g\}$
	- I think of it as 5 ways to pick the first element, 4 the second, and 3 the third; then divide by two to get rid of the 1+1s that are equal
* **1+1+1+1**: there are **5** sets: $\{r,b,g,p\},\ldots\{b,g,p,o\}$

So there are **70 possible plates**
### stars and bars

I don't think I'd ever been introduced to the [stars and bars](https://en.wikipedia.org/wiki/Combination#Example_of_counting_multisubsets) method before. With this, we can observe that to draw any plate, we need to draw four items from five bins. So we might represent a plate $\{r,r,p,o\}$ as:

$$\star \star |\,\,|\,\,| \star | \star$$
Which is to say, two items from the $r$ bin, none from $b$ or $g$, then one each from $p$ and $o$.

The stars and bars method says that we can sum up the sets as
$$\dbinom{stars+bars}{stars} = \dbinom{8}{4} = \frac{8!}{4!*(8-4)!} = \frac{8!}{4!4!} = \frac{8*7*6*5}{24} = 70$$

### general answer

The number of multisets of size $k$ from $n$ choices is given by $\dbinom{n+k-1}{k}$, which in this case is $\dbinom{8}{4} = 70$, the same equation we solved above for the stars and bars method.

# Napkin approximation

On a given draw¹, we do **36** comparisons from only **70** possible plates, so there's a **51.4% chance** that two plates are equivalent.

# The problem

There are two problems with our approximation:
- all 70 plates are not equally likely. It is **24x more likely** that we draw a 1+1+1+1 set than that we draw a set of 4 same tiles
- we solved for the **expected number of matches** in a round, not the likelihood of having any matched plate

In this case, it's actually quite close to the real answer, by chance, because the two errors roughly cancel each other out.

### set distribution

There are **625** total possible arrangements of the 5 tiles, which we can calculate with $5!$.

There are only **5** different arrangements 

To fix it, we start by observing that there are **625** ($5!$) possible arrangements of the tiles, taking order into account

$$\sum P(\text{plate})^2 = \frac{1}{625^2}\Big(5{\cdot}1 + 20{\cdot}16 + 10{\cdot}36 + 30{\cdot}144 +
5{\cdot}576\Big)$$

Numerator: $5 + 320 + 360 + 4320 + 2880 = 7885$

$$P(\text{match}) = \frac{7885}{390625} \approx 0.02019 \approx \frac{1}{49.5}$$

¹: given the simplifying assumptions that we can draw them from an infinite bag of tiles and that the distribution of plates is uniform
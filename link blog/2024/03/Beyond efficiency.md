https://www.cs.unm.edu/~ackley/be-201301131528.pdf
alt: https://cacm.acm.org/opinion/beyond-efficiency/

> Esteem for efficiency should be tempered with respect for robustness.

...

> To see how robustness and efficiency can trade off, consider sorting a list by comparing pairs of items... imagine sorting just 52 items, like a shuffled deck of cards... Each algorithm picks pairs of cards to compare, and passes them to a ‘card comparison component’ to determine their order.
> 
> Here’s the twist: Imagine that component is _unreliable_. Maybe malware corrupted it. Maybe sunspots cooked it. We don’t know why. For this demonstration, the card comparison component usually works fine, but on 10% of comparisons it gives a random answer.

> Averaged over 1,000 shuffled decks, here are the errors made by each sorting algorithm:

![[Pasted image 20240304095101.png]]
> Bubble sort’s inefficient repeated comparisons repair many faults, and its inefficient short moves minimize the damage of the rest.

...

> It is time to study and manage incorrectness in the interest of robustness. We should not shun the trade-off, but rather, we should understand, engineer, and teach computation beyond correctness and efficiency only.

> Robust-first computation now.

- David Ackley

via [Lu Wilson](https://futureofcoding.org/episodes/070) (I haven't listened to the podcast, just got the link from the notes)
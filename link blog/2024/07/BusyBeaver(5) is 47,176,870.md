---
created: 2024-07-02T14:14:33.606Z
updated: 2024-07-02T14:14:33.606Z
---
> Only now, after an additional 41 years, do we know the _fifth_ Busy Beaver value... BB(5) is equal to 47,176,870—the value that’s been _conjectured_ since 1990, when Heiner Marxen and Jürgen Buntrock [discovered](https://turbotm.de/~heiner/BB/mabu90.html) a 5-state Turing machine that runs for exactly 47,176,870 steps before halting, when started on a blank tape. The new bbchallenge achievement is to prove that all 5-state Turing machines that run for more steps than 47,176,870, actually run forever—or in other words, that 47,176,870 is the maximum _finite_ number of steps for which any 5-state Turing machine can run. That’s what it means for BB(5) to equal 47,176,870.

- [Scott Aaronson](https://scottaaronson.blog/?p=8088)

I like to follow along with computer science achievements when I can, and this one is super easy to state in the abstract: BB(5) is the maximum number of steps a 5 state Turing machine with two symbols can run, and still halt.

The details of course, are more challenging, and Scott's article does a great job sketching out some of them.

One fun note he mentions is that BB(6) is known to be at least 10 raised to itself 15 times, the wonderful number:

$10^{10^{10^{10^{10^{10^{10^{10^{10^{10^{10^{10^{10^{10^{10}}}}}}}}}}}}}}$

Scott links a few other sources:

- [Quanta](https://www.quantamagazine.org/amateur-mathematicians-find-fifth-busy-beaver-turing-machine-20240702)
- [bbchallenge](https://discuss.bbchallenge.org/t/july-2nd-2024-we-have-proved-bb-5-47-176-870/237) (the online organization that coordinated the effort)
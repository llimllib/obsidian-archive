---
created: 2024-05-23T00:28:15.844Z
updated: 2024-05-23T00:28:15.844Z
---
https://www.quantamagazine.org/computer-scientists-invent-an-efficient-new-way-to-count-20240516/

An article describing the algorithm given in [this paper](https://drops.dagstuhl.de/storage/00lipics/lipics-vol244-esa2022/LIPIcs.ESA.2022.34/LIPIcs.ESA.2022.34.pdf) by Chakraborty, Vinochandran, and Meel.

Donald Knuth also posted [an article](https://cs.stanford.edu/~knuth/papers/cvm-note.pdf) about the algorithm.

The basic idea seems to be that it's an extremely simple, probabalistic version of [[hyperLogLog]]; Stephan Hügel offers [this very short implementation](https://github.com/urschrei/cvmcount/blob/main/src/lib.rs).
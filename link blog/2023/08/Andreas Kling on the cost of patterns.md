---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
> ~2 years ago I became convinced that meticulously checking every heap allocation for failure would lead to robust GUI applications that don't fall apart under resource pressure. 
> 
> Fast-forward to today, we have made the SerenityOS codebase significantly uglier and less pleasant to work on as a direct result of pursuing this goal. 
> 
> At the same time, the sought-after robustness remains a hypothetical mirage. 
> 
> It's time to admit I was wrong about this. Not because it's impossible, but because it's costing us way more than it's giving us. 
> 
> On reflection, I believe the main mistake here was adopting the meticulous checks wholesale across the entire operating system. It should have instead been limited to specific, critical services and libraries. 
> 
> Adopting new patterns is easy. Admitting that you adopted the wrong pattern and reversing course is harder. However, I now believe we need to walk backwards a bit to make GUI programming on SerenityOS fun again.

in a [tweet](https://twitter.com/awesomekling/status/1690769829198704640?s=12), via [jado](https://notado.app/feeds/jado/software-development). I again miss twitter, and am sad for the good stuff that's getting posted there that I can't see any longer.

It is really hard to admit that a pattern you've followed such as this is not worth the benefit, and it's even harder to back it out without losing coherence in a large codebase.
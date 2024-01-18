https://codahale.com/work-is-work/

was reminded of this post by [this tweet](https://nitter.net/apenwarr/status/1747068908929192432#m); I'd read it before but it was pre-linkblog. One of my all-time favorite articles on system/culture/business design.

(The list of good articles in that category is, sadly, not large)

> we can sketch out the _boundaries_ of what an organization is capable of and the dynamics of that as it grows... modeling organizations as parallel processes can inform the way we design them.

> What happens inside those boundaries is a matter of execution and effort; what happens outside those boundaries is impossible.

> **The work capacity of an organization scales, at most, linearly as new members are added.** Each new member in an organization adds a constant number of possible work hours to the total possible work hours of the company’s existing employees. [Amdahl’s Law](https://en.wikipedia.org/wiki/Amdahl%27s_law) states that given a fixed task, a parallel solution utilizing NN processors will run faster than a sequential solution by _at most_ a factor of NN.

---

> As an organization hires more employees, work on productivity improvements must be a constant priority. Internal tooling, training, and services must be developed and fielded to ensure that all members are able to work on problems of continuously increasing impact. **The ceaseless pursuit of force multipliers is the only possible route to superlinear productivity improvements as an organization grows.**

---

> **Contention costs grow superlinearly as new members are added.** Parallel solutions to tasks are rarely perfectly concurrent (and indeed, such tasks are rightfully called “embarrassingly parallel”), and often require some sequential critical sections.

> ...At some point, adding new members can cause the organization’s overall productivity to decrease instead of increase, as the increase in wait time due to contention is greater than the increase in work capacity. (This is the organizational version of the latency spikes we see as servers become overloaded.)

> These shared resources aren’t necessarily physical things, like bathrooms or printers; they can be digital, like files in a source code repository or tickets in a bug tracker, or organizational, like code reviews or work assignments. As with writing highly-concurrent applications, building high-performing organizations requires a careful and continuous search for shared resources, and developing explicit strategies for mitigating their impact on performance.

I pride myself on being a person that finds and eliminates these shared contention points, but that's not something I know how to express on a CV, and it often leaves me in a position of having to explain to somebody what, exactly, it is I do here. Wonder how I could do better at that

---

> While some organizations are chattier than others, this communication is essential for the sharing of information and the coordination of action. But it’s not free. Communication takes time. If the relative percentage of people who need to talk to each other to get something done stays constant as the organization grows (i.e., x%x% of all dyads), **the total time spent communicating will grow quadratically as the work capacity of the organization grows linearly**.

> ...In terms of organizational design, this means limiting both the types and numbers of consulted constituencies in the organization’s process. Each additional person or group in a [responsibility assignment matrix](https://en.wikipedia.org/wiki/Responsibility_assignment_matrix) geometrically increases the area of that matrix. Each additional responsibility assignment in that matrix geometrically increases the cost of organizational coherence.

---

> Principles From Beyond Space and Time:

> - Keep the work parallel, the groups small, and the resources local
> - Prioritize the development of force multipliers
> - If possible, factor work products into independent modules, if not, grow slowly and optimize
> - Scale organizational efforts across a portfolio of synergistic products
> - Keep responsibility assignment matrices small, sparse, and local
> - Prioritize asynchronous information distribution over synchronous
> - What happenns inside the boundaries is important
---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/tigerbeetledb/tigerbeetle/blob/main/docs/TIGER_STYLE.md

A very interesting document by the TigerBeetle db team laying out their style and axioms.

> -   Use **only very simple, explicit control flow** for clarity. **Do not use recursion** to ensure that all executions that should be bounded are bounded. Use **only a minimum of excellent abstractions** but only if they make the best sense of the domain. Abstractions are [never zero cost](https://isaacfreund.com/blog/2022-05/). Every abstraction introduces the risk of a leaky abstraction.

> -   **Put a limit on everything** because, in reality, this is what we expect—everything has a limit. For example, all loops and all queues must have a fixed upper bound to prevent infinite loops or tail latency spikes. This follows the [“fail-fast”](https://en.wikipedia.org/wiki/Fail-fast) principle so that violations are detected sooner rather than later. Where a loop cannot terminate (e.g. an event loop), this must be asserted.

> -   **Assert all function arguments and return values, pre/postconditions and invariants.** A function must not operate blindly on data it has not checked. The purpose of a function is to increase the probability that a program is correct. Assertions within a function are part of how functions serve this purpose. The assertion density of the code must average a minimum of two assertions per function.

> -   **The golden rule of assertions is to assert the _positive space_ that you do expect AND to assert the _negative space_ that you do not expect** because where data moves across the valid/invalid boundary between these spaces is where interesting bugs are often found. This is also why **tests must test exhaustively**, not only with valid data but also with invalid data, and as valid data becomes invalid.

> -   All memory must be statically allocated at startup. **No memory may be dynamically allocated (or freed and reallocated) after initialization.** This avoids unpredictable behavior that can significantly affect performance, and avoids use-after-free. As a second-order effect, it is our experience that this also makes for more efficient, simpler designs that are more performant and easier to maintain and reason about, compared to designs that do not consider all possible memory usage patterns upfront as part of the design.

> -   **Perform back-of-the-envelope sketches with respect to the four resources (network, disk, memory, CPU) and their two main characteristics (bandwidth, latency).** Sketches are cheap. Use sketches to be “roughly right” and land within 90% of the global maximum.

Found via Paul linking to ["A database without dynamic memory"](https://tigerbeetle.com/blog/a-database-without-dynamic-memory/) 

I wrote a short twitter thread on it [here](https://twitter.com/llimllib/status/1580593215354175503)
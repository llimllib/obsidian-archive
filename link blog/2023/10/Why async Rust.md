---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://without.boats/blog/why-async-rust/

I don't write rust, but this detailed discussion of the history and reasons for the design of async rust is very interesting to read.

> People implementing highly performant network services in languages without facilities for user-space concurrency like C tend to implement them using a hand-written state machine. This is exactly what the Future abstraction was designed to compile into, but without having to write the state machine by hand: the whole point of the coroutine transform is to write imperative code “as if your function never yields,” but have the compiler generate the state transitions to suspend it when it would block. The benefits of this are not insignificant.

----

> It was clear, though usually left unsaid, that what Rust needed to succeed was industry adoption, so that it could continue to receive support once Mozilla stopped being willing to fund an experimental new language. And it was clear that the most likely path to short-term industry adoption was in network services, especially those with a performance profile that compelled them at the time to be written in C/C++. This use case fit the niche of Rust perfectly - these systems need high degrees of control to achieve their performance requirements but avoiding exploitable memory bugs is critical because they are exposed to the network.
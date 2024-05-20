---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
Intro to Part 1:

> Our overall goal is to understand the root causes of _variance_ in transaction latency - the apparently random unexpectedly long repsonse times in comlex software

> This part also introduces the important practice of estimating within a factor of 10 how long pieces of code should take

# Chapter 1

Definitions:

- {transaction, query, request} - an input message to a computer system that must be dealt with as a single unit of work
- server - a computer processing transactions
- {latency, response time} - the time elapsed between sending a message and receiving its result
- offered load - the number of transactions sent per second
- service - a collection of programs that ahndle one particular kind of transaction
- tail latency - the slowest transsctions in the distrubution of response times for a service
- dynamics - the activity over time for a collection of programs; what pieces of code run when, what they wait for, what memory space they take, and how different programs affect each other
	- As programmers we often have an image in our head of what the dynamics are, and performance problems are often due to a difference between theis picture and the reality of the dynamics
	- if we observe the true dynamics, we can adjust our mental picture and usually improve the code's performance with simple changes
- cache hit - finding and reusing software-cached data
- cache miss - failing to do so
- remote procedure call  (RPC) - network message passing or remote procdure calls between programs. May be synchronous or asynchronous.

> The median (or similar average) latency is a particularly ill-suited description of a skewed or multi-peak distribution because it rarely is near many of the actual values and it tells us nothing about the shape and size of the long tail - our topic of interest

```
                 Expectations───────────┐
                                        │
                                        │
                ┌─────────┐             │
┌─────────┐     │ System  │       ┌─────▼──────┐       ┌─────────┐    ┌────┐
│ Offered ├─────►  Under  ├───────►Observations├───────►Reasoning├────►Fix │
│  load   │     │  Test   │       └────────────┘       └─────────┘    └────┘
└─────────┘     └─────────┘
```

## Order-of-Magnitude Estimates

- In this book, we'll use the notation _O(n)_ for "on the order of _n_", with the _units_ always specified
- nsec: nanoseconds (1 billionth of a second)
- usec: microseconds (1 millionth of a second)
- msec: milliseconds (1 thousandth of a second)

### Numbers every programmer should know

Action | Time | O(n)
-------|------|-----
L1 cache reference | .5 nsec | O(1) nsec
Branch mispredict | 5 nsec | O(10) nsec
L2 cache reference | 7 nsec | O(10) nsec
Mutext lock/unlock | 25 nsec | O(10) nsec
Main memory reference | 100 nsec | O(100) nsec
Compress 1k bytes with zippy | 3000 nsec | O(1) usec
Send 2k bytes over 1Gbps network | 20,000 nsec | O(10) usec
Read 1mb sequentially from memory | 250,000 nsec | O(100) usec
Round trip within same datacenter | 500,000 nsec | O(1) msec
Disk seek | 10,000,000 nsec | O(10) msec
Read 1mb sequentially from disk | 20,000,000 nsec | O(10) msec
Send packet CA -> Netherlands -> CA | 150,000,000 nsec | O(100) msec

> Doing an order of magnitude estimate of expected times in various parts of a program makes it easy, when you get real measurements of those times, to spot ones that differ substantially from your expectations. **This is where the learning is**

- Once we trace the slowness to a layer N of a network that's not waiting on layer N+1, we want to observe that layer in more detail. Either the slow RPC is doing _extra work_ or  they are doing normal work but _executing slowly_
	- usually in the first case, we can replicate the problem offline in a testing environment
	- References ["System Performance" by Gregg](https://www.amazon.com/gp/product/B08J5QZPNC) for observation tools that can be used to trace the problem
- We're interested in this book in the second case - an RPC doing just the normal work but more slowly than usual
	- something is _interfering_ with the RPC's normal work on a single server
	- we call these _hindered_ transactions
	- usually do not occur in offline testing, but only when running a live user-facing load
	- in this environment, observation tools that slow down processing by 2x or even 10% are too slow to be used
		- we need observation techniques with <1% overhead
			- there are very few of these available - pt III introduces one

### The five fundamental resources
- intereference on a single server must come from something on that server (incl. incoming and outgoing network traffic)... comes almost exclusively from contention for a shared resource

There are only four computer hardware resources shared between unrelated programs running on a single server:
- CPU
- Memory
- Disk/SSD
- Network

If a program has multiple cooperating threads, there is a fifth fundamental resource:
- Software critical section
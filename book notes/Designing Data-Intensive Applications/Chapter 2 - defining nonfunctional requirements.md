---
created: 2026-04-20T15:17:14.922Z
updated: 2026-04-20T15:17:14.922Z
---
The authors define a *functional requirement* as "the functionality that the application must offer", and the *nonfunctional requirements* as everything else you need to do.

Right off the bat, I struggle with this definition! They give performance as an example of a nonfunctional requirement, but obviously that's a matter of degree. Let's see if they clarify, or just allow the definition to be very fuzzy at the edges.

## Twitter example

They start off with a motivating example, of a common interview question: let's design a service like twitter. Given three tables:

| users | id  | screen_name | profile_image |
| ----- | --- | ----------- | ------------- |
|       | 12  | jack        | 123.png       |

| posts | id  | sender_id fk(users) | timestamp | text                     |
| ----- | --- | ------------------- | --------- | ------------------------ |
|       | 20  | 12                  | 123456    | just setting up my twttr |

| follows | follower_id fk(users) | followee_id fk(users) |
| ------- | --------------------- | --------------------- |
|         | 9923882               | 12                    |

They give the first pass SQL query to create a timeline page:

```sql
SELECT posts.*, users.* 
  FROM posts
  JOIN follows ON posts.sender_id = follows.followee_id
  JOIN users   ON posts.sender_id = users.id
 ORDER BY posts.timestamp DESC
 LIMIT 1000
```

This query will be expensive, so we will in practice need to materialize the timeline. For each user, we store their home timeline; when a user posts, we look up all their followers and insert that post into their timeline.

_fan-out_ means the factor by which the number of requests increases in such a scenario.

### describing performance

Two main types of performance metric:
- *response time* - the elapsed time from a request to a response
- _throughput_ - the requests per second the system is processing

Generally, response time decreases as throughput increases.

They have a brief sidebar about using jitter and exponential backoff plus circuit breakers to avoid thundering herd issues, but don't dive into it.

> response time is usually what users care about the most, whereas the throughput determines the required computing resources

- _response time_ is what the client sees; includes all delays anywhere in a system
- _service time_ is the duration for which the service is actively processing the client's request
- _queueing delays_ they don't define, oddly, just put it in italics and assume its definition is understood
- _latency_ is a catchall term for time during which a request is not being actively processed (i.e. during which it is latent)
	- This is interesting to me because they make latency a relativistic measurement; it matters if, from your perspective, you know that work is being done on it
	- We can call response time "request latency" because it's time when we (the client) don't know that the request is being actively processed (or we can say that it is not being actively processed by our system)
		- the author gives "network latency" as a particular example - `the time that a request and response spend traveling through the network`, but from the network stack's perspective, there are several different times within that span when the request is latent, and others when it's workign on it

There's a brief discussion of median/mean/percentiles

> Amazon describes response time requirements for internal services in terms of the 99.9th percentile... Optimizing the 99.99th percentile (the slowest 1 in 10,000 requests) was deemed too expensive and found to not yield enough benefit

The authors point to several sources for the "performance == money" idea, and suggest that they're all insufficient and somewhat contradictory, and that we don't really know how much performance is functional, in the sense of making more money from users.

They point to [the tail at scale](https://cacm.acm.org/research/the-tail-at-scale/) to describe _tail latency amplification_, whereby as a single service request makes more and more requests to other endpoints, it becomes more likely that one of them suffers a tail latency spike.

There's a brief discussion of how SLOs and SLAs may use percentiles to define their expectations, and an important sidebar that averaging percentiles is **meaningless**. I've seen people make that mistake many times in practice, and it's possible I have (I certainly have (sorry))

### reliability and fault tolerance

_reliability_ is, roughly, continuing to work correctly, even when things go wrong

They distinguish betwen _faults_ and _failures_:
- A _fault_ occurs when a particular _part_ of a system stops working correctly
- A _failure_ occurs when the system _as a whole_ stops providing the required service to the user

> They are the same thing at different levels

I'm glad they said that, it was my immediate objection to that definition!

We call a system _fault-tolerant_ if it continues providing the required service to users in spite of faults occurring, and a part is a _single point of failure_ if failure causes failure to the whole system.

> Counterintuitively, in fault-tolerant systems, it can make sense to _increase_ the rate of faults by triggering them deliberately -- for example, by randomly killing individual processes without warning. This is called _fault injection_... by deliberately inducing faults, you ensure that the fault-tolerance machinery is continually exercised and tested

### Hardware and software faults

> Hardware redundancy increases the uptime of a single machine... using a distributed system has advantages, such as being able to tolerate a complete outage of one datacenter. For this reason, ccloud systems tend to focus less on the reliability of individual machines and instead aim to make services highly available by tolerating faulty nodes at the software level. Cloud providers use _availability zones_ to identify which resources are physically co-located

hardware failures are often less correlated than software faults, because it is common for many nodes to run the same software and thus have the same bugs

### Human beings

> One study of large internet services found that configuration changes by operators were the leading cause of outages, whereas hardware faults played a role in only 10-25% of cases \[[72](https://www.usenix.org/legacy/events/usits03/tech/full_papers/oppenheimer/oppenheimer_html/index.html)]

ed: that study is from 2003, I wonder if there's anything more recent

> What we call "human error" is... a symptom of a problem with the sociotechnical system in which people are trying their best to do their jobs

They cite "the field guide to understanding human error", which I had for a while but failed to read

### Scalability

_Scalability_ is the term we use to describe a system's ability to cope with increased load


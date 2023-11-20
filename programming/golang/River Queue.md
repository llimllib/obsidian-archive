https://github.com/riverqueue/river
https://riverqueue.com/

> Fast and reliable background jobs in Go.

> Atomic, transaction-safe, robust job queueing for Go applications. Backed by PostgreSQL and built to scale.

From [the hn thread](https://news.ycombinator.com/item?id=38349716):

> Transactional job queues have been a recurring theme throughout my career as a backend and distributed systems engineer at Heroku, Opendoor, and Mux. Despite the problems with non-transactional queues being well understood I keep encountering these same problems. I wrote a bit about them here in our docs: [https://riverqueue.com/docs/transactional-enqueueing](https://riverqueue.com/docs/transactional-enqueueing)

> Ultimately I want to help engineers be able to focus their time on building a reliable product, not chasing down distributed systems edge cases. I think most people underestimate just how far you can get with this model—most systems will never outgrow the scaling constraints and the rest are generally better off not worrying about these problems until they truly need to.
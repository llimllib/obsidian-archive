[k6](https://k6.io/)
- recommended by the fly.io team as the best web perf tester they know of

[ab](https://httpd.apache.org/docs/2.4/programs/ab.html) (aka apachebench)
- the classic, there seem to be better tools these days though

[wrk](https://github.com/wg/wrk)

> wrk is a modern HTTP benchmarking tool capable of generating significant load when run on a single multi-core CPU. It combines a multithreaded design with scalable event notification systems such as epoll and kqueue.

[wrk2](https://github.com/giltene/wrk2) 

> wrk2 is wrk modifed to produce a constant throughput load, and accurate latency details to the high 9s (i.e. can produce accurate 99.9999%'ile when run long enough). In addition to wrk's arguments, wrk2 takes a throughput argument (in total requests per second) via either the --rate or -R parameters (default is 1000).

[hey](https://github.com/rakyll/hey)

> hey is a tiny program that sends some load to a web application.

[vegeta](https://github.com/tsenart/vegeta)

> Vegeta is a versatile HTTP load testing tool built out of a need to drill HTTP services with a constant request rate. It can be used both as a command line utility and a library.

(ed: a go library)

[locust](https://locust.io/)

> Define user behaviour with Python code, and swarm your system with millions of simultaneous users.

we used this to good success on MCT

[fortio](https://github.com/fortio/fortio)

> Fortio runs at a specified query per second (qps) and records an histogram of execution time and calculates percentiles (e.g. p99 ie the response time such as 99% of the requests take less than that number (in seconds, SI unit)). It can run for a set duration, for a fixed number of calls, or until interrupted (at a constant target QPS, or max speed/load per connection/thread).

> Fortio is a fast, small (4Mb docker image, minimal dependencies), reusable, embeddable go library as well as a command line tool and server process, the server includes a simple web UI and REST API to trigger run and see graphical representation of the results (both a single latency graph and a multiple results comparative min, max, avg, qps and percentiles graphs).

> Fortio also includes a set of server side features (similar to httpbin) to help debugging and testing: request echo back including headers, adding latency or error codes with a probability distribution, tcp echoing, tcp proxying, http fan out/scatter and gather proxy server, GRPC echo/health in addition to http, etc...

----

[Summary of the options as of 2020](https://k6.io/blog/comparing-best-open-source-load-testing-tools/), by an author of k6 - still a good reasonably fair article

> -   I like **Hey** in the "I need a simple command-line tool to hit a single URL with some traffic" use case.
> -   I like **Vegeta** in the "I need a more advanced command-line tool to hit some URLs with traffic" use case.
> -   I like **k6** (obviously) in the "automated testing for developers" use case.
> -   I like **Locust** in the "I'd really like to write my test cases in Python" use case.
> -   I like **Wrk** in the "just swamp the server with tons of requests already!" use case.
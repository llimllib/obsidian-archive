---
updated: '2024-04-17T15:06:09Z'
created: '2023-10-20T13:54:09Z'
---
## good_job

https://github.com/bensheldon/good_job

> **Inspired by [Delayed::Job](https://github.com/collectiveidea/delayed_job) and [Que](https://github.com/que-rb/que), GoodJob is designed for maximum compatibility with Ruby on Rails, ActiveJob, and Postgres to be simple and performant for most workloads.**

-   **Designed for ActiveJob.** Complete support for [async, queues, delays, priorities, timeouts, and retries](https://edgeguides.rubyonrails.org/active_job_basics.html) with near-zero configuration.
-   **Built for Rails.** Fully adopts Ruby on Rails [threading and code execution guidelines](https://guides.rubyonrails.org/threading_and_code_execution.html) with [Concurrent::Ruby](https://github.com/ruby-concurrency/concurrent-ruby).
-   **Backed by Postgres.** Relies upon Postgres integrity, session-level Advisory Locks to provide run-once safety and stay within the limits of `schema.rb`, and LISTEN/NOTIFY to reduce queuing latency.
-   **For most workloads.** Targets full-stack teams, economy-minded solo developers, and applications that enqueue 1-million jobs/day and more.

## sidekiq

https://github.com/mperham/sidekiq

> Simple, efficient background processing for Ruby.

> Sidekiq uses threads to handle many jobs at the same time in the same process. It does not require Rails but will integrate tightly with Rails to make background processing dead simple.

Requires redis (IIRC), and has the largest community of all rails job runners

## que

https://github.com/que-rb/que

What we use on people app. Simple and gets the job done with postgres.

## delayed_job

https://github.com/collectiveidea/delayed_job

Not dead, but pining for the fjords per the author on news.yc

## faktory

https://contribsys.com/faktory/
https://github.com/contribsys/faktory

From the people (er, Mike Perham) that brought you `sidekiq`, faktory is a language-agnostic job server. Like sidekiq, has an OSS and a Pro level; you need pro to get cron jobs, statsd metrics, and all kinds of other stuff you're probably going to want.
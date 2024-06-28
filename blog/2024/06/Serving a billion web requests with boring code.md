---
created: 2024-06-24T17:32:45.949Z
updated: 2024-06-24T17:32:45.949Z
---
- [High level](#high-level)
- [Boring über alles](#boring-uber-alles)
- [The boring bits](#the-boring-bits)
	* [Why React?](#why-react)
	* [golang](#golang)
- [The innovation tokens](#the-innovation-tokens)
	* [Modular backend](#modular-backend)
	* [gRPC](#grpc)
- [Strict backwards compatibility](#strict-backwards-compatibility)
- [Faceted search](#faceted-search)
- [Database](#database)
	* [creation](#creation)
	* [ETL](#etl)
	* [models](#models)
	* [testing](#testing)
	* [Local database for development](#local-database-for-development)
- [Miscellaneous tooling](#miscellaneous-tooling)
- [Logging](#logging)
- [Documentation](#documentation)
- [Runtime integrations](#runtime-integrations)
- [And more](#and-more)

When I worked as a contractor to the US government at [ad hoc](adhocteam.us), I was fortunate enough to get the opportunity to design large parts of a relaunch of [medicare plan compare](https://www.medicare.gov/plan-compare/), the US government site through which hundreds of thousands of medicare recipients purchase their health care plans each year.

We released after about a year of development, and were able to help millions of people find and purchase health care - if you're in the US, you are pretty likely to know somebody who used this system.

Though the US health care system is incredibly awful in many respects, I'm very proud of what the team I worked with was able to build in a short time frame and under a lot of constraints.

The team of people that I worked with - managers, designers, engineers and business analysts - were excellent from top to bottom. I've never before experienced such a dedicated, collaborative, trusting team, and I learned a tremendous amount from them.

I especially want to share this story because I want to show that quality software can get written under government constraints. It can! And if we all start believing that it can, we're more likely to produce it.

## High level

I worked on this system for about two and a half years, from the very first commit through two open enrollment periods. 

The API system served about 5 million requests on a normal weekday, with < 10 millisecond average request latency and a 95th percentile latency of less than 100 milliseconds.

It served a very low baseline rate of errors, mostly spurious errors due to vulnerability scrapers. I'm proud that I can count the number of times an engineer was woken up by an emergency page on one hand.

I was amazed at how far you can get by leaning on postgres and golang, keeping your system as organized and simple as possible, and putting in work every day for a long period of time.

## Boring über alles

My north star when building the system was to keep it as boring as possible, in the [Dan McKinley sense](https://mcfunley.com/choose-boring-technology). (Go read "Choose Boring Technology" if you haven't yet, it's required reading. It's better than this article.)

There is a concept of "Innovation tokens" in that article, and I was explicit in choosing the pieces I used to build the site with how I spent them.

## The boring bits

- **postgres** - The rock on which I prefer to build my systems
- **golang** - I had experience with it from working on [healthcare.gov](https://changelog.com/gotime/154), and felt extremely confident in its reliability and relative simplicity
- **react** - React is boring in the sense we're discussing here, it's extremely widely deployed and was known well by my teammates

### Why React?

There are many valid criticisms of react; [this piece](https://infrequently.org/2021/03/the-performance-inequality-gap/) is an example, and I was aware of the issues already in 2018 when I was building the site. The main thrust is that it tends towards large application bundles, which take a long time to download and execute, especially on the cheap mobile phones that are the main link to the internet for so many people.

In building a piece of infrastructure for the government, it was especially concerning that the application be available to as many people as possible. We took accessibility seriously both in the sense that the site needed to have proper design for users with disabilities and also in the sense that people with many devices needed to connect to it.

Nevertheless, I chose an SPA architecture and react for the site.

I would have loved to have done differently, but I worried that choosing to use a multi-page architecture or a different library would have slowed us down enough that we wouldn't have delivered on our tight timeline. I didn't have enough trust in any of the alternatives available to me at the time to make me believe we could choose them safely enough.

The result fell prey after a few years to a common failure mode of react apps, and became quite heavy and loaded somewhat slowly.

I still think I made the right choice at the time, but it's unfortunate that I felt I had to make it and I wish I had known of a nice clean way to avoid it.

### golang

Golang was overall a joy to build this project in. It runs efficiently both at build time and at run time, and having binary executable artifacts that build quickly makes it easy to deploy rapidly.

Developers new to the language (our team of engineers grew from 2 to 15) were able to get onboard quickly and understand the language with no trouble.

Error handling being both immediate and verbose is, in my opinion, a great feature for building systems that are resilient. Every time you do something that might fail, you are faced with handling the error case, and once you develop patterns they are consistent and predictable. (I know this is a big topic, I should probably write more about it)

The day that we were able to switch to go modules, a big pain point went away for us. We hit a few bumps in the road as very early adopters but it was worth it.

My biggest gripe with the golang ecosystem was that the documentation generation for projects that are not public sucks. For a long time, the documentation generator didn't even support projects that used modules.

That said, I was overwhelmingly happy with my choice here and never regretted it.

## The innovation tokens

I made two architectural bets that I was less confident of than the others:

- **Modular backend** - I designed the backend neither as microservices, nor as a monolith, but into three large modules
- **GRPC** - The backend services communicated with each other via GRPC, and with web clients via [grpc-gateway](https://github.com/grpc-ecosystem/grpc-gateway)

### Modular backend

I split the backend up into three parts; they all lived in the same repository but were designed such that they could be pulled apart and given to a new team if necessary.

Each component had its own postgres database (which were physically co-located, but never intertwined) and strictly used gRPC to communicate between themselves.

The split was largely based around data access patterns:
#### drug pricing (aka druginfo)

One thing the site needed to be able to do was estimate the cost of any packaging variation of any drug at any pharmacy on any health insurance plan. Easy, right?

This combinatorial explosion (I once calculated how many trillions of possibilities this was) necessitated a very carefully-indexed database, a large amount of preprocessing, and a commitment to engineering with performance in mind.

It took a long time and a ton of government health system reverse engineering to figure out how to get even close to right with this part. I'm forever indebted to my colleagues who dove deep into the depths of [CMS](https://www.cms.gov/)  bureaucracy, and then turned it into documentation and code.
#### plan search (aka planinfo)

The main purpose of the site was for people to search for and purchase medicare part C and part D health care plans.

Every day, we'd get a new dump of detailed health care plan information from CMS; this module would load the information into a new postgres database, and then we'd deploy a new version pointing at the new day's data.

Both `planinfo` and `druginfo` had entirely immutable databases in this way; their only job was to serve an API based on the most recent data for each.

#### beneficiary information (aka beneinfo)

In the insurance argot, a person on a health care plan is a "beneficiary" of the plan. It sounds a little self-important to me, but that's just what it is I suppose.

(One thing I tried to do throughout my work on this project was to use the proper industry jargon wherever possible rather than something more familiar to myself. I felt it was part of the commitment to boringness to keep the jargon friction down to a minimum.)

The job of the `beneinfo` module was to store information about plan customers, and was the only part of the application where the database was long-lived and mutable.

We strove to store as little data as possible here, to minimize the risk should there be any data leakage, but there was no way around storing a very scary amount of Personally Identifiable Information (PII). We were as serious as possible about this data, and the risk of losing control of it kept me nervous at all times.

### gRPC

Overall, gRPC was not as great for us as I'd hoped when beginning the project.

The best benefit of using it, and the driver behind my choice to use it, was that every interface was specified in code. This was very useful; we could generate tools and interfaces that changed in lockstep.

The biggest pain points were all related to the tooling. I maintained a set of very hairy makefiles with eldritch `protoc` commands to build all the interfaces into go files that we could use, and debugging those was always painful.

Not being able to curl the system, as we would if it were a JSON API, was a pain in the butt. `grpcurl` existed, and we used it, but was not nearly as nice.

[grpc-gateway](https://github.com/grpc-ecosystem/grpc-gateway) was the best part of the ecosystem I used, it served more than a billion requests for us and was never once the source of a problem. It enabled us to do what gRPC ought to have been able to do from the start, serve requests to web clients.

I loved having interface schemas, but we used so few of gRPC's features and the code generation was so complicated that we probably would have been slightly better off without it.

## Strict backwards compatibility

We followed a strict backwards-compatibility requirement, and only added and never removed fields from our interfaces. Once a field was exposed in the public API, it would be exposed forever unless it became a security problem (which, thankfully, never happened to us in the years I worked on this project).

We did the same with the databases as the API; columns were added and rarely removed. If a column actually merited removal, the process was to add a column, remove all references to the old one, _wait a few weeks to make sure we didn't need to roll back_, then finally remove the column from the database.

Our discipline with backwards compatibility gave us freedom to keep up a high rate of changes and maintain confidence that local changes would not have negative downstream consequences.

## Faceted search

A core principle of the app was to rely on postgres whenever possible, and also to be stupid instead of clever whenever possible.

Faceted search was an excellent example of both of those properties. We could have reached for elasticsearch, and we also could have tried to use an ORM, or built a little faceting language.

We implemented faceted search by having a well-indexed table of plans, and building a SQL query string by tacking on conditions based on a long series of conditions.

The function `buildQuery` which implemented the core part of this scheme is a single 250 line function, heavily commented, which lays out the logic in a nearly flat way. The focus is kept squarely on business requirements, instead of on fancy code.

## Database
###  creation

We stored the database schemas in a series of `.sql` files with leading numbers, so that they could be loaded in order at database creation time.

For `planinfo` and `beneinfo`, there were no migrations, because the database was recreated every day. Instead, there was a `version` number stored in both the database and the application. Given that we (tried very hard to) never make backwards incompatible changes to the database, the apps would check at startup that their database schema version number was greater than or equal to the database version number stored in the database, and refuse to start if they were not.

This was **a general pattern**: If an app encountered any unexpected or missing configuration, it refused to start and threw noticeable, hopefully clear, errors. 

I tried hard to make it so that if the apps actually started up, they would have everything they needed to run properly.

There were occasional instances where we accidentally rolled out backwards-incompatible changes to the database, and in those cases we generally rolled back the data update and rebuilt it.
### ETL

The part of the system I'm most proud of, and on which I spent the most effort, is the ETL process.

We had a series of shell scripts for each data source we ingested (there were many), which would pull the data and put it in an s3 bucket.

Then, early in the morning, a cron job would spin up an EC2 instance, which would pull in the latest ETL code and all the data files. It would spin up a new database in our RDS instance, and begin the ETL process.

If things went well, right about the time the east coasters got into work, a new database would be rotating into service.

My recollections are not exact, but it took something like two to four hours to generate a new database with more than 250 million rows out of several gigabytes of text files in various formats.

The code to insert data into the database heavily utilized [postgres' `COPY`](https://www.postgresql.org/docs/current/sql-copy.html) statement, avoiding `INSERT`s as much as possible in favor of generating batches of collections that could be `COPY`ed into the database.

###  models

We used the [xo](https://github.com/xo/xo) library to connect to the database and generate models, along with heavily customized templates.

The templates themselves, and the code to create the models from them was hairy. Thankfully it mostly only had to be written once and occasionally edited.
### testing

Here was **my biggest mistake**: I invested a great deal of time and effort in creating [sql-mock](https://github.com/DATA-DOG/go-sqlmock) tests for data that changed regularly. These tests needed constant, tedious maintenance.

I should instead have tested against a live database, especially given that we were working mostly with immutable databases and wouldn't have had to deal with recreating it for each test.
### Local database for development

Each table in the database had an accompanying script that would generate a subset of the data for use in local development, since the final database was too large to run on a developer's machine.

This let each developer work with a live, local, copy of the database and enabled efficient development of changes.

I highly recommend building in this tooling from the start, it saves you from either trying to add it in once your database grows large, or having your team connect to a remote database, making development slower.
## Miscellaneous tooling

We had a CLI tool, written mostly as a bunch of shell scripts, with a ton of available commands that performed all kinds of utility functions related to observability and operations.

It was mostly written by an excellent coworker, and working with it is where I learned to write effective shell scripts. (Thanks to Nathan and [shellcheck](https://www.shellcheck.net/) for this vital skill).

Having this available from the start served as a really useful place for utility features to coalesce; without it they tend to scatter to more places further afield, or just live in a developer's shell history.

One fun bit of tooling I build was the ability to generate graphs from splunk via slack commands, which was particularly helpful in incident handling, as you could easily share graphs with your coworkers.

## Logging

Every request that entered the backend got a request id as soon as it hit the system, and that request id was carried around with it wherever it went. Middleware gave the request its id, and then another middleware constructed a sub-logger with the request id embedded into it that was attached to the request context, so that all logs always had the request ID attached.

The system logged on entry and exit, with as much detail as was safe. Any other logging that was above the debug level was supposed to be exceptional, although we weren't super strict about that.

We used [zerolog](https://pkg.go.dev/github.com/rs/zerolog), and it worked great for us.
## Documentation

At some point, I converted the markdown docs I and others had written in github into a book about how the system worked, using [sphinx-book-theme](https://sphinx-book-theme.readthedocs.io/en/stable/tutorials/get-started.html).

Miraculously, this book gained traction, and I got great contributions from teammates and everybody knew where to look to find system documentation.

I have started documentation websites for many other projects, and no other ones have ever worked as successfully, and I wish that I had any idea why that was but I don't.

It proudly featured our mascot (the corgi) showing off its most notable feature

![[Pasted image 20240627221817.png]]
## Runtime integrations

Our client frequently wanted us to add queries that would operate from the browser, and I was fortunate to be able to push back and turn many of those into build-time requests instead.

Once place where our performance got killed at our clients' request was with render-blocking analytics scripts; it seemed every team wanted a different script run to get the analytics that they "needed". I advised them against it and tried to demonstrate the performance and download size problems they incurred, but the client was not interested in my arguments.

## And more

There are so many more parts of a system like this that I haven't covered here; I mostly wanted to write down a bit about a bunch of the pieces while I still remember what they are.

I was very fortunate to be able to work with such a positive, creative, and engaged team that made the space for such a successful project to be possible. An article about the social factors and personalities that made the team go, and the site happen, would be a second article as long as this one is.
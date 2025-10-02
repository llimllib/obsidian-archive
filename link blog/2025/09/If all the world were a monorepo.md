---
created: 2025-09-30T13:19:04.267Z
updated: 2025-09-30T13:19:04.267Z
---
https://jtibs.substack.com/p/if-all-the-world-were-a-monorepo

> As a software engineer raised on a traditional diet of C, Java, and Lisp, I’ve found myself downright baffled by R. I’m no stranger to mastering new programming languages, but learning R was something else: it felt like studying Finnish after a lifetime of speaking Romance languages...

> In the years since, my discomfort has given away to fascination. I’ve come to respect R’s bold choices, its clarity of focus, and the R community’s continued confidence to ‘do their own thing’...

The "if the world were a monorepo" bit means that when you submit a library to CRAN, they check to see if it breaks the tests of any other packages, and won't let you publish until it doesn't

> The world of R packages is like a huge monorepo. When declaring dependencies, most packages don’t specify any version requirements, and if they do, it’s usually just a lower bound like ‘grf >= 1.0’. This lets a user just sit down at their computer, update all the packages in their environment to the latest versions, and resume their work, much like you would perform a ‘git pull’ in a single repo.

> CRAN’s approach clearly puts a burden on package developers, and in my experience, can materially slow down the release of new versions. But it results in an excellent workflow for R’s central user base: the researchers and data scientists who want to spend as much time as possible on the details of data analysis, not stuck in transitive dependency hell2.

It's a very interesting inversion of burden from developers to library maintainers instead!
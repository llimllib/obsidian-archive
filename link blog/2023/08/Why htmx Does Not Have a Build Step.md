---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://htmx.org/essays/no-build-step/

> The best reason to write a library in plain JavaScript is that it lasts forever. This is arguably JavaScript’s single most underrated feature. While I’m sure there are some corner cases, JavaScript from 1999 that ran in Netscape Navigator will run unaltered, alongside modern code, in Google Chrome downloaded yesterday.

> ...Maintenance is a cost paid for with labor, and open-source codebases are the projects that can least afford to pay it. Opting not to use a build step drastically minimizes the labor required to keep htmx up-to-date. This experience has been borne out by [intercooler.js](https://intercoolerjs.org), the predecessor to htmx which is maintained indefinitely with (as I understand) very little effort. When htmx 1.0 was released, TypeScript was at version 4.1; when intercooler.js was released, TypeScript was pre-1.0. Would code written in those TypeScript versions compile unmodified in today’s TypeScript compiler (version 5.1 at the time of writing)? Maybe, maybe not.

> ...Modularization is one of the [honking great ideas](https://legacy.python.org/dev/peps/pep-0020/) of software. Modules make it possible to solve incredibly complex problems by breaking down code into well-contained substructures that solve smaller problems. Modules are really useful.

> Sometimes, however, you want to solve simple problems, or at least relatively simple problems. In those cases, it can be helpful _not_ to use the building blocks of more complex software, lest you emulate their complexity without creating commensurate value. At its core, htmx solves a relatively simple problem: it adds a handful of attributes to HTML that make it easier to replace DOM elements using the declarative character of hypertext. Requiring that htmx remain in a single file (again, around 3,500 LOC) enforces a degree of intention on the library; there is a real pressure when working on the htmx source to justify the addition of new code, a pressure which maintains an equilibrium of relative simplicity.

Reminds me a lot of Sqlite's aesthetics and minimal build process.
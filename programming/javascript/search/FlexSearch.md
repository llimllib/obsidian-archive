https://github.com/nextapps-de/flexsearch

> Web's fastest and most memory-flexible full-text search library with zero dependencies.

> When it comes to raw search speed [FlexSearch outperforms every single searching library out there](https://nextapps-de.github.io/flexsearch/bench/) and also provides flexible search capabilities like multi-field search, phonetic transformations or partial matching.

> Depending on the used [options](https://github.com/nextapps-de/flexsearch#options) it also provides the [most memory-efficient index](https://github.com/nextapps-de/flexsearch#memory). FlexSearch introduce a new scoring algorithm called ["contextual index"](https://github.com/nextapps-de/flexsearch#contextual) based on a [pre-scored lexical dictionary](https://github.com/nextapps-de/flexsearch#dictionary) architecture which actually performs queries up to 1,000,000 times faster compared to other libraries. FlexSearch also provides you a non-blocking asynchronous processing model as well as web workers to perform any updates or queries on the index in parallel through dedicated balanced threads.

found via tmcw starring it

see also [[pagefind]]

----

I switched this site's notes over to it ([1](https://github.com/llimllib/obsidian_notes/commit/e1ff77a8706532b1aaf1c164ffb2e2dcc61282f3) [2](https://github.com/llimllib/obsidian_notes/commit/2488a2d7346be06cb94149f0cda4ccfc5195eaf9#diff-d6af0459a37d985953d7040c14f53feb3b9cc9e58b543aa3c2b80256d276c5e0R566-R576)), and it kind of stinks that flexsearch doesn't return the index of matches back to you. If you want to highlight matched terms, you have to implement that yourself.

However, the results are definitely better.
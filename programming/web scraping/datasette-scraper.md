https://datasette.io/plugins/datasette-scraper

> `datasette-scraper` is a Datasette plugin to manage small-ish (~100K pages) crawl and extract jobs.

-   Opinionated yet extensible
    -   Some useful tasks are possible out-of-the-box, or write your own pluggy hooks to go further
-   Leans heavily into SQLite
    -   Introspect your crawls via ops tables exposed in Datasette
-   Built on robust libraries
    -   [Datasette](https://datasette.io/) as a host
    -   [selectolax](https://github.com/rushter/selectolax) for HTML parsing
    -   [httpx](https://www.python-httpx.org/) for HTTP requests
    -   [pluggy](https://pluggy.readthedocs.io/en/stable/) for extensibility
    -   [zstandard](https://github.com/indygreg/python-zstandard) for efficiently compressing HTTP responses

> **Not for adversarial crawling**. Want to crawl a site that blocks bots? You're on your own.
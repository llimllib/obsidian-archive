---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/ericchiang/pup

> pup is a command line tool for processing HTML. It reads from stdin, prints to stdout, and allows the user to filter parts of the page using [CSS selectors](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Getting_started/Selectors).

> Inspired by [jq](http://stedolan.github.io/jq/), pup aims to be a fast and flexible way of exploring HTML from the terminal.

I wanted to turn a "best of" list into a comment I could post on reddit, here's the command I used:

1. download the page: `curl https://post-trash.com/news/2022/4/7/post-trashs-year-in-review-the-best-of-2022 > /tmp/post-trash.html`
2. parse out the titles, remove blank lines, and convert HTML entities to ascii:
```
| pup '.summary-title text{}' | \
    grep -v -e '^\s*$' | \
    python3 -c 'import html, sys; [print(html.unescape(l), end="") for l in sys.stdin]'
```
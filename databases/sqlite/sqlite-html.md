---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/asg017/sqlite-html

https://observablehq.com/@asg017/introducing-sqlite-html

> [sqlite-html](https://github.com/asg017/sqlite-html) is a new SQLite extension for querying, manipulating, and generating HTML.

> `sqlite-html` is an alternative to other HTML parsers like [htmlq](https://github.com/mgdm/htmlq), [BeautifulSoup](https://www.crummy.com/software/BeautifulSoup/bs4/doc/), and [Cheerio](https://cheerio.js.org/), with the added benefit of a full SQL API. Simply [load the extension](https://github.com/asg017/sqlite-html#as-a-loadable-extension) in your SQLite client of choice, and start parsing HTML with CSS selectors.

truly brilliant. Example:

```sql
select
  html_text(items.html, "strong") as name,
  html_attr_get(
    html_extract(items.html, 'a[href*=".zip"]'),
    'a',
    'href'
  ) as href
 from html_each(
  (select page from pages where name = 'lacounty-results'),
  '.expandable_item.indent'
) as items
```

It would be interesting to try replacing my beautiful soup scripts in [[NBA Stats]] with this tool.

Built in golang, with [goquery](https://github.com/PuerkitoBio/goquery) (library for html selectors) and [riyaz-ali/sqlite](https://github.com/riyaz-ali/sqlite) (library for building sqlite extensions in go)
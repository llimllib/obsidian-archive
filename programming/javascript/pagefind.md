https://pagefind.app/
https://github.com/CloudCannon/pagefind/

> Pagefind is a fully static search library that aims to perform well on large sites, while using as little of your users’ bandwidth as possible, and without hosting any infrastructure.

> ...The goal of Pagefind is that websites with tens of thousands of pages should be searchable by someone in their browser, while consuming a reasonable amount of bandwidth. Pagefind’s search index is split into chunks, so that searching in the browser only ever needs to load a small subset of the search index. Pagefind can run a full-text search on a 10,000 page site with a total network payload under 300KB, including the Pagefind library itself. For most sites, this will be closer to 100KB.

The search engine appears to be a [rust application](https://github.com/CloudCannon/pagefind/tree/1ea1e75c3254899f40a80a740ad829fd00df14dd/pagefind/src) built to a wasm bundle. It looks like it builds an index of the site, creates a bunch of page files, and then when you search it checks the index for what the relevant pages are, downloads only those ones, and serves results.

via [Carl M. Johnson](https://mastodon.social/@carlmjohnson/111024763667968055) on mastodon

see also [[flexsearch]]
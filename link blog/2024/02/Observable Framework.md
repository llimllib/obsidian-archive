https://observablehq.com/blog/observable-2-0

https://observablehq.com/framework/

Observable Framework is built around the pattern of regularly updating a static website with data that is downloaded and compiled at build time.

> Today we’re launching [Observable 2.0](https://observablehq.com/product) with a bold new vision: an open-source static site generator for building fast, beautiful data apps, dashboards, and reports.

---
> Framework’s data loaders solve this “last mile” problem by computing static data snapshots at build time. These snapshots can be highly-optimized (and aggregated and anonymized), minimizing the data you send to the client. And since a data loader is just a fancy way of generating a file on-demand (with clever caching and routing), loaders can be written in any language and use any library. This flexibility is not unlike [CGI](https://en.wikipedia.org/wiki/Common_Gateway_Interface) from 30 years ago, and [Unix pipes](https://en.wikipedia.org/wiki/Pipeline_(Unix)). And since data loaders run on your servers, viewers don’t need direct access to the underlying data sources, and your dashboards are more secure and robust.
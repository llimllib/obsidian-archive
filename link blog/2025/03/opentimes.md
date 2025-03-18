https://opentimes.org

> Today I’m launching [OpenTimes](https://opentimes.org), a free database of pre-computed, point-to-point travel times between major U.S. Census geographies. In addition to letting you [visualize travel isochrones](https://opentimes.org), OpenTimes also lets you download massive amounts of travel time data for free and with no limits. Visit the dedicated [about page](https://opentimes.org/about) to learn more about the project.

- [Dan Snow](https://sno.ws/opentimes/)

Very cool!

> The entire OpenTimes backend is just static Parquet files on [Cloudflare’s R2](https://www.cloudflare.com/developer-platform/products/r2/). There’s no RDBMS or running service, just files and a CDN. The whole thing costs about $10/month to host and costs nothing to serve. In my opinion, this is a _great_ way to serve infrequently updated, large public datasets at low cost (as long as you partition the files correctly).
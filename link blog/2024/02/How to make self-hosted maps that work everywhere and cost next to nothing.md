---
updated: '2024-03-12T15:15:06Z'
created: '2024-02-26T15:30:45Z'
---
https://www.muckrock.com/news/archives/2024/feb/13/release-notes-how-to-make-self-hosted-maps-that-work-everywhere-cost-next-to-nothing-and-might-even-work-in-airplane-mode/

> Over the past few years, an emerging ecosystem of open-source tools has made self-hosting a map stack both viable and affordable. Beyond cost, self-hosting creates a level of security and durability that’s hard to find with third-party services, which are always at risk of being bought, shut down or simply broken by neglect.

What's funny to me is that this is almost exactly how Paul Smith started off his [article in 2008](https://alistapart.com/article/takecontrolofyourmaps/) extolling the virtues of building and hosting your own maps. 16 years later, nothing has changed: most people use hosted services but a few have seen how it's reasonable to make and host your own maps.

Paul's article was what first got me interested in making custom maps, which has been a hobby for me for some time now, so I hope this article does the same for a newer generation.

The article suggests:
- getting data from [[pmtiles]], using the [extract command](https://docs.protomaps.com/pmtiles/cli#extract) to pull a region from the [global daily builds](https://maps.protomaps.com/builds/) that give the full OSM tiles for the world
- Using [[Tippecanoe]] to bake your data into the tile extract
	- mentions [[planetiler]] and [[tilemaker]] as options
- use [[MapLibre]] to display the map
- fly.io, R2 or google pages for hosting

links to [simon willison's similar article](https://til.simonwillison.net/gis/pmtiles), [[Serving a custom vector web map using PMTiles and maplibre-gl]]

links to [this github repo, implementing a demonstration workflow](https://github.com/sfchronicle/nicar23-map-tiles-demo)

[here is a similar repo](https://github.com/eyeseast/self-hosted-maps-codespace) to that one, a self-hosted map setup with [[pmtiles]] and [[Tippecanoe]]

see also [[create your own vector tiles]]

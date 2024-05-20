---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/protomaps/go-pmtiles

>  Single-file executable tool for creating, reading and uploading PMTiles archives 

- convert mbtiles to pmtiles
- extract a region or zoom level from a pmtiles file
- inspect pmtiles files
- serve pmtiles
	- including from cloud storage

reminded of it by [this toot](https://elk.pwm.social/hachyderm.io/@bdon@mastodon.social/111050304115215000):

> extracted this multipolygon from a 100GB planet #openstreetmap tileset served over HTTPS:

> * zooms 0-15
> * 15 million total tiles, ~15GB output
> * 1000 HTTP requests
> * 4 minutes download (60,000 tiles per second) across the ocean

> small extract areas - like this circle around Washington DC - complete in about 15 seconds (30 MB tileset)
https://www.openstreetmap.org/user/rtnf/diary/400836

Walks through creating a small [[PMTiles]] vector map using [josm](https://josm.openstreetmap.de) [tippecanoe](https://github.com/mapbox/tippecanoe) and [go-pmtiles](https://github.com/protomaps/go-pmtiles)

- josm to export a subset of OSM data to geojson
- tippecanoe to render it to a vector mbtiles file
- [[go-pmtiles]] to convert it to pmtiles
- render it on the web with [maplibre-gl](https://maplibre.org/maplibre-gl-js-docs/api/)
	- An OSS fork of mapbox-gl.
	- [github here](https://github.com/maplibre/maplibre-gl-js)
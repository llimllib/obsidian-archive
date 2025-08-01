---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/topojson/topojson

> **TopoJSON** is an extension of [[GeoJSON]] that encodes topology. Rather than representing geometries discretely, geometries in TopoJSON files are stitched together from shared line segments called _arcs_. This technique is similar to [Matt Bloch’s MapShaper](http://www.cartogis.org/docs/proceedings/2006/bloch_harrower.pdf) and the [Arc/Info Export format, .e00](https://web.archive.org/web/20140721114041/http://indiemaps.com:80/blog/2009/02/e00parser-an-actionscript-3-parser-for-the-arcinfo-export-topological-gis-format/).

> TopoJSON eliminates redundancy, allowing related geometries to be stored efficiently in the same file. For example, the shared boundary between California and Nevada is represented only once, rather than being duplicated for both states. A single TopoJSON file can contain multiple feature collections without duplication, such as states and counties. Or, a TopoJSON file can efficiently represent both polygons (for fill) and boundaries (for stroke) as two feature collections that share the same arc mesh.

> ...As a result, TopoJSON is substantially more compact than GeoJSON, frequently offering a reduction of 80% or more even without simplification. Yet encoding topology also has numerous useful applications for maps and visualization above! It allows [topology-preserving shape simplification](https://github.com/topojson/topojson-simplify), which ensures that adjacent features remain connected after simplification; this applies even across feature collections, such as simultaneous consistent simplification of state and county boundaries. Topology can also be used for [Dorling](http://www.ncgia.ucsb.edu/projects/Cartogram_Central/types.html) or [hexagonal cartograms](http://pitchinteractive.com/latest/tilegrams-more-human-maps/), as well as other techniques that need shared boundary information such as [automatic map coloring](https://bl.ocks.org/4188334).

Is also a set of command-line tools for manipulating topojson files
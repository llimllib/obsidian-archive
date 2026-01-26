---
created: 2026-01-26T13:04:47.115Z
updated: 2026-01-26T13:04:47.115Z
---
[[MapLibre]] announces that they have a new tile format, MapLibre Tile (MLT) to replace Mapbox Vector Tiles (MVT)

> MLT is specifically designed for modern and next-generation graphics APIs to enable high-performance processing and rendering of large (planet-scale) 2D and 2.5 basemaps. This current implementation offers feature parity with MVT[1](https://maplibre.org/news/2026-01-23-mlt-release/#user-content-fn-1) while delivering on the following:
> 
> - **Improved compression ratio**: up to 6x on large tiles, based on a column-oriented layout with recursively applied (custom) lightweight encodings. This leads to reduced latency, storage, and egress costs and, in particular, improved cache utilization.
> - **Better decoding performance**: fast, lightweight encodings that can be used in combination with SIMD/vectorization instructions.

They can be generated with [[planetiler]] or [this code](https://github.com/maplibre/maplibre-tile-spec/tree/main/java/encoding-server) that converts MVT to MLT in real time
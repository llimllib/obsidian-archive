---
created: 2026-04-09T20:28:55.979Z
updated: 2026-04-09T20:28:55.979Z
---
https://github.com/Query-farm/geosilo

> A [[DuckDB]] extension for compact geometry encoding. Delta-encodes coordinates as scaled integers instead of float64 pairs, achieving **3–4x smaller** geometry on disk and over the wire compared to standard WKB. Points compress to just **9 bytes** (vs 21 bytes WKB).

> GeoSilo provides a first-class `GEOSILO` column type with transparent interop — standard `ST_*` spatial functions work directly on GEOSILO columns, with high-performance native implementations for common operations that skip the WKB decode step entirely.
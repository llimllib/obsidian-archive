---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
[xid](https://github.com/rs/xid) provides a quality hash, based on MongoDB's object ID hash.

> Features:

-   Size: 12 bytes (96 bits), smaller than UUID, larger than snowflake
-   Base32 hex encoded by default (20 chars when transported as printable string, still sortable)
-   Non configured, you don't need set a unique machine and/or data center id
-   K-ordered
-   Embedded time with 1 second precision
-   Unicity guaranteed for 16,777,216 (24 bits) unique ids per second and per host/process
-   Lock-free (i.e.: unlike UUIDv1 and v2)

> Best used with [zerolog](https://github.com/rs/zerolog)'s [RequestIDHandler](https://godoc.org/github.com/rs/zerolog/hlog#RequestIDHandler).

(linking [[zerolog]])

ported to many languages.
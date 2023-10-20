https://github.com/ulid/spec

> UUID can be suboptimal for many use-cases because:

-   It isn't the most character efficient way of encoding 128 bits of randomness
-   UUID v1/v2 is impractical in many environments, as it requires access to a unique, stable MAC address
-   UUID v3/v5 requires a unique seed and produces randomly distributed IDs, which can cause fragmentation in many data structures
-   UUID v4 provides no other information than randomness which can cause fragmentation in many data structures


A neat feature of the ULID is that it includes the date of its creation - which means you can do things like say "if this key is older than X, do legacy thing"

(comes from [this thread](https://twitter.com/__steele/status/1570208081296134145) about AWS best practices)
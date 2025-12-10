---
created: 2025-12-10T13:48:09.416Z
updated: 2025-12-10T13:48:09.416Z
---
https://github.com/durable-streams/durable-streams

> While durable streams exist throughout backend infrastructure (database WALs, Kafka topics, event stores), they aren't available as a first-class primitive for client applications. There's no simple, HTTP-based durable stream that sits alongside databases and object storage as a standard cloud primitive.

> WebSocket and SSE connections are easy to start, but they're fragile in practice: tabs get suspended, networks flap, devices switch, pages refresh. When that happens, you either lose in-flight data or build a bespoke backend storage and client resume protocol on top...

> **Durable Streams addresses this gap.** It's a minimal HTTP-based protocol for durable, offset-based streaming designed for client applications across all platforms: web browsers, mobile apps, native clients, IoT devices, and edge workers. Based on 1.5 years of production use at [Electric](https://electric-sql.com/) for real-time Postgres sync, reliably delivering millions of state changes every day.

Neat-looking library that aims to solve a problem I've experienced.

I've not tried it out.

Released by [electric SQL](https://electric-sql.com/blog/2025/12/09/announcing-durable-streams) (cf [[electric]])
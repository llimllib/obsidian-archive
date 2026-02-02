---
created: 2026-02-02T03:29:02.271Z
updated: 2026-02-02T03:29:02.271Z
---
https://github.com/DataDog/pg_tracing

> pg_tracing is a PostgreSQL extension that generates server-side spans for distributed tracing.

![[Pasted image 20260201222931.png]]

> When pg_tracing is active, it generates spans on sampled queries. To access these spans, the extension provides two ways:
> 
>     pg_tracing_consume_spans and pg_tracing_peek_spans views output spans as a set of records
>     pg_tracing_json_spans function outputs spans as a OTLP json
> 
> The utility functions pg_tracing_reset and pg_tracing_info provide ways to read and reset extension's statistics. These are not available globally but can be enabled for a specific database with CREATE EXTENSION pg_tracing.
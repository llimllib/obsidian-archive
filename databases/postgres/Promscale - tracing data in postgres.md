https://www.timescale.com/blog/observability-powered-by-sql-understand-your-systems-like-never-before-with-opentelemetry-traces-and-postgresql/

timescaleDB has an open source product that lets you ingest opentracing data into postgres:

> You're probably thinking that observability data is time-series data that relational databases struggle with once you reach a particular scale. Luckily, PostgreSQL is highly flexible and allows you to extend and improve its capabilities for specific use cases. [TimescaleDB builds on that flexibility to add time-series superpowers to the database](https://docs.timescale.com/timescaledb/latest/overview/how-does-it-compare/timescaledb-vs-postgres/#much-higher-ingest-rates) and scale to millions of data points per second and petabytes of data.

> Today, we are announcing the general availability of OpenTelemetry tracing support in [Promscale](https://www.timescale.com/promscale), the observability backend for metrics and traces built on the rock-solid foundations of PostgreSQL and TimescaleDB. We’re now closer to becoming the unified data store for observability powered by SQL, bringing the PostgreSQL and observability worlds together.
---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/VictoriaMetrics/VictoriaMetrics
https://victoriametrics.com/

> VictoriaMetrics is a fast, cost-effective and scalable monitoring solution and time series database.

> - It can be used as long-term storage for Prometheus. See these docs for details.
> - It can be used as a drop-in replacement for Prometheus in Grafana, because it supports Prometheus querying API.
> - It can be used as a drop-in replacement for Graphite in Grafana, because it supports Graphite API.
> - It features easy setup and operation:
>     - VictoriaMetrics consists of a single small executable without external dependencies.
>     - All the configuration is done via explicit command-line flags with reasonable defaults.
>     - All the data is stored in a single directory pointed by -storageDataPath command-line flag.
>     - Easy and fast backups from instant snapshots can be done with vmbackup / vmrestore tools. See this article for more details.
> - It implements PromQL-like query language - MetricsQL, which provides improved functionality on top of PromQL.

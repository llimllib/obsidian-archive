---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://brycemecum.com/2023/03/31/til-mermaid-tracing/

clever re-use of gantt charts as trace diagrams.

> Today I noticed via [a tweet](https://twitter.com/mitsuhiko/status/1641040644121436160) by [@mitsuhiko](https://twitter.com/mitsuhiko) that [Mermaid](https://mermaid.js.org/) Gantt diagrams are great for displaying distributed trace information like what you’d get from [JaegerUI](https://github.com/jaegertracing/jaeger-ui).

![[Pasted image 20230401113153.png]]

```
gantt
    title Trace Showing Attached and Detached Spans
    dateFormat x
    axisFormat %S.%L

    section Frontend
    /checkout               :crit, 0, 500ms
    App                     :300, 180ms
    POST /api/analytics     :done, 450, 70ms
    GET /assistant/poll     :done, 450, 120ms
    POST /api/analytics     :done, 580, 70ms
```
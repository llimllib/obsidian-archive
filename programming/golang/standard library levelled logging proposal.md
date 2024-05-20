---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/golang/go/discussions/54763

> Our goals are:

> -   Ease of use. A survey of the existing logging packages shows that programmers want an API that is light on the page and easy to understand. This proposal adopts the most popular way to express key-value pairs, alternating keys and values.
    
> -   High performance. The API has been designed to minimize allocation and locking. It provides an alternative to alternating keys and values that is more cumbersome but faster (similar to [Zap](https://pkg.go.dev/go.uber.org/zap)'s `Field`s).
    
> -   Integration with runtime tracing. The Go team is developing an improved runtime tracing system. Logs from this package will be incorporated seamlessly into those traces, giving developers the ability to correlate their program's actions with the behavior of the runtime.


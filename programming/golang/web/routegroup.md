---
created: 2024-07-29T17:42:41.269Z
updated: 2024-07-29T17:42:41.269Z
---
https://github.com/go-pkgz/routegroup

> routegroup is a tiny Go package providing a lightweight wrapper for efficient route grouping and middleware integration with the standard http.ServeMux.

```go
mux := http.NewServeMux()
group := routegroup.New(mux)

// adding routes with middleware
group.Use(loggingMiddleware, corsMiddleware)
group.Handle("/hello", helloHandler)
group.Handle("/bye", byeHandler)

// nested route groups
apiGroup := routegroup.Mount(mux, "/api")
apiGroup.Use(loggingMiddleware, corsMiddleware)
apiGroup.Handle("/v1", apiV1Handler)
apiGroup.Handle("/v2", apiV2Handler)
```
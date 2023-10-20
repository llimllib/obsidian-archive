https://github.com/colega/zeropool

> `zeropool` is a zero-allocation type-safe `sync.Pool`

```go
// The function provided to zeropool.New() makes a Pool of a correct type using generics.
pool := zeropool.New(func() []byte { return nil })

// This is a []byte, no need to make type-assertion, no need to de-reference.
buf := pool.Get()

// This does not allocate.
pool.Put(buf)
```

> [Go provides](https://pkg.go.dev/sync#Pool) `sync.Pool` pool implementation that allows storing `any` values (`interface{}` values). It is great but has two major drawbacks:

> -   It's not type-safe, a type-assertion is needed on the elements provided by `Get()`.
> -   Since it stores `interface{}` values, it means that your value will escape[1](https://github.com/colega/zeropool#user-content-fn-1-e1353ead5d2e3a7e8f7307dc8141f07b) to the heap unless you store a pointer (it would escape, but maybe just once).
https://github.com/samber/lo

> ✨ samber/lo is a Lodash-style Go library based on Go 1.18+ Generics.
> 
> This project started as an experiment with the new generics implementation. It may look like Lodash in some aspects. I used to code with the fantastic "go-funk" package, but "go-funk" uses reflection and therefore is not typesafe.
> 
> As expected, benchmarks demonstrate that generics are much faster than implementations based on the "reflect" package. Benchmarks also show similar performance gains compared to pure for loops. See below.
> 
> In the future, 5 to 10 helpers will overlap with those coming into the Go standard library (under package names slices and maps). I feel this library is legitimate and offers many more valuable abstractions.

```go
names := lo.Uniq[string]([]string{"Samuel", "John", "Samuel"})
// []string{"Samuel", "John"}
```

```go
import "github.com/samber/lo"

lo.Map([]int64{1, 2, 3, 4}, func(x int64, index int) string {
    return strconv.FormatInt(x, 10)
})
// []string{"1", "2", "3", "4"}
```

I'm not sure I would use this in production code, but I'd be tempted for sure
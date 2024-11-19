---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/sourcegraph/conc

> `conc` is your toolbelt for structured concurrency in go, making common tasks easier and safer.

> The main goals of the package are:

> 1.  Make it harder to leak goroutines
> 2.  Handle panics gracefully
> 3.  Make concurrent code easier to read

> In `conc`, the owner of a goroutine is always a `conc.WaitGroup`. Goroutines are spawned in a `WaitGroup` with `(*WaitGroup).Go()`, and `(*WaitGroup).Wait()` should always be called before the `WaitGroup` goes out of scope.

references [[Go statement considered harmful]] in the README 😍

cf [[flowmatic]], which looks nicer but I've never used either
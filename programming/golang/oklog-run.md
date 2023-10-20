https://pkg.go.dev/github.com/oklog/run#section-readme

> run.Group is a universal mechanism to manage goroutine lifecycles.

> Create a zero-value run.Group, and then add actors to it. Actors are defined as a pair of functions: an **execute** function, which should run synchronously; and an **interrupt** function, which, when invoked, should cause the execute function to return. Finally, invoke Run, which concurrently runs all of the actors, waits until the first actor exits, invokes the interrupt functions, and finally returns control to the caller only once all actors have returned. This general-purpose API allows callers to model pretty much any runnable task, and achieve well-defined lifecycle semantics for the group.

Used this to great success in MCT.

I think I initially found it via [[Peter Bourgon on organizing concurrent go]]


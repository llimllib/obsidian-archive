https://github.com/jonboulle/clockwork

> Replace uses of the `time` package with the `clockwork.Clock` interface instead.

> For example, instead of using `time.Sleep` directly:

```go
func myFunc() {
	time.Sleep(3 * time.Second)
	doSomething()
}
```
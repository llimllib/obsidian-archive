https://pkg.go.dev/github.com/rogpeppe/go-internal/testscript

Used by the golang test suite, and now broken out into a package, it asserts command output and includes full files.

For example, this script asserts that "cat" prints `hello world` to stdout and nothing to `stderr` (I think, if I'm reading it right!)

```bash
# hello world
exec cat hello.text
stdout 'hello world\n'
! stderr .

-- hello.text --
hello world
```

found via https://encore.dev/blog/testscript-hidden-testing-gem ; I had seen it in the golang source before but never bothered to look at it in more detail.

A good model of creating tests that match your app.
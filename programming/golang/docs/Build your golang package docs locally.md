---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://mdaverde.com/posts/golang-local-docs/

> Similar to my Rust setup, I wanted to see a rendering of my module docs as they would on [pkg.go.dev](https://pkg.go.dev/) **locally before publishing**. This used to be [possible](https://stackoverflow.com/a/13530336/1879774) with `godoc` but it's been [deprecated](https://github.com/golang/go/issues/49212) since then with no official solution.

> The recommendation now is to point users to [pkgsite](https://github.com/golang/pkgsite/tree/master/cmd/pkgsite) (the tool used to render pkg.go.dev) but it's left as an [exercise to the user](https://github.com/golang/go/issues/40371) on exactly what the setup should be.

> So let's do the exercise.

The golang documentation situation is awful and not improving, sadly
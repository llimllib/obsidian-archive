https://ko.build/

> `ko` is a simple, fast container image builder for Go applications.

> It's ideal for use cases where your image contains a single Go application without many dependencies on the OS base image (e.g., no cgo, no OS package dependencies).

> `ko` builds images by executing `go build` on your local machine, and as such doesn't require `docker` to be installed. This can make it a good fit for lightweight CI/CD use cases.

> `ko` makes [multi-platform builds](https://ko.build/features/multi-platform/) easy, produces [SBOMs](https://ko.build/features/sboms/) by default, and includes support for simple YAML templating which makes it a powerful tool for [Kubernetes applications](https://ko.build/features/k8s/).
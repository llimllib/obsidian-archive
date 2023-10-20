https://github.com/google/ko

`ko` is a simple, fast container image builder for [[golang]] applications.

It's ideal for use cases where your image contains a single Go application without any/many dependencies on the OS base image (e.g., no cgo, no OS package dependencies).

`ko` builds images by effectively executing `go build` on your local machine, and as such doesn't require `docker` to be installed. This can make it a good fit for lightweight CI/CD use cases.
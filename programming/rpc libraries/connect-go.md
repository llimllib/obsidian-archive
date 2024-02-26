https://github.com/bufbuild/connect-go
https://connectrpc.com/docs/introduction

> Connect is a slim library for building browser and gRPC-compatible HTTP APIs. You write a short [Protocol Buffer](https://developers.google.com/protocol-buffers) schema and implement your application logic, and Connect generates code to handle marshaling, routing, compression, and content type negotiation. It also generates an idiomatic, type-safe client. Handlers and clients support three protocols: gRPC, gRPC-Web, and Connect's own protocol.

> The [Connect protocol](https://connect.build/docs/protocol) is a simple, POST-only protocol that works over HTTP/1.1 or HTTP/2. It takes the best portions of gRPC and gRPC-Web, including streaming, and packages them into a protocol that works equally well in browsers, monoliths, and microservices. Calling a Connect API is as easy as using `curl`. Try it with our live demo:

```
curl \
    --header "Content-Type: application/json" \
    --data '{"sentence": "I feel happy."}' \
    https://demo.connect.build/buf.connect.demo.eliza.v1.ElizaService/Say
```

written in [[go]]

There's also a package for generating [typescript bindings](https://www.npmjs.com/package/@bufbuild/connect-web)
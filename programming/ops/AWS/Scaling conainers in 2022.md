---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
[Excellent article](https://www.vladionescu.me/posts/scaling-containers-on-aws-in-2022/) on the different methods for running a container on AWS, and how they scale.

I'm honestly less interested in how they scale and more interested in how they perform/cost, which sadly this article doesn't get into, but it's very good anyway.

confirms my belief that ECS on fargate is currently the simplest/best approach for most apps that should be considered the default, but I'm hopeful for App Runner to become more usable/cheaper in the future.

Found via [this tweet](https://twitter.com/iamvlaaaaaaad/status/1514234438527643656)

[this is the app they deployed](https://github.com/poc-hello-world/namer-service) to all the different services

[this repo contains the terraform they used](https://github.com/vlaaaaaaad/blog-scaling-containers-on-aws-in-2022) to deploy to each of the services

[this is the docker build GHA action](https://github.com/docker/build-push-action) they used to build all the containers
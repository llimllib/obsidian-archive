---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
Appears to be AWS' attempt at doing Cloud Run?

https://aws.amazon.com/apprunner/

> AWS App Runner is a fully managed service that makes it easy for developers to quickly deploy containerized web applications and APIs, at scale and with no prior infrastructure experience required. Start with your source code or a container image. App Runner builds and deploys the web application automatically, load balances traffic with encryption, scales to meet your traffic needs, and makes it easy for your services to communicate with other AWS services and applications that run in a private Amazon VPC. With App Runner, rather than thinking about servers or scaling, you have more time to focus on your applications.

appears not to scale to zero, unfortunately: https://github.com/aws/apprunner-roadmap/issues/9

Looks like according to their page a basic app would run about $25/mo, not including whatever database or other infra fees: https://aws.amazon.com/apprunner/pricing/

They show a dev app costing $5/mo, but that's with manually stopping and starting it every time it gets used, which seems pretty silly
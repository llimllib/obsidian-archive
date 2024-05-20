---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/digma-ai/digma

> In short, we can use existing logs, traces and metrics to answer questions such as:

-   Where is this function called from? Is it even used?
-   Is this a problematic area of the code? Where are my bottlenecks?
-   What type of errors does this code raise in runtime? What issues are escalating? Which are affecting the end user?

Digma ingests OpenTracing data and tries to show useful things about your code in context, I guess:

![](https://miro.medium.com/max/1400/1*fsdlOBsc_Oxql-uBIeD-jw.png)

Seems pretty neat; found via [this article](https://betterprogramming.pub/improving-code-design-with-opentelemetry-a-practical-guide-a08e6440c24d) "# Improving Code Design With OpenTelemetry — A Practical Guide" which walks you through setting up Jaeger, Digma and OpenTelemetry traces in a sample app.
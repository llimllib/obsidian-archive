https://dl.acm.org/doi/pdf/10.1145/3593856.3595909

> When writing a distributed application, conventional wisdom says to split your application into separate services that can be rolled out independently. This approach is well-intentioned, but a microservices-based architecture like this often backfires, introducing challenges that counteract the benefits the architecture tries to achieve. Fundamentally, this is because microservices conflate logical boundaries (how code is written) with physical boundaries (how code is deployed). 
> 
> In this paper, we propose a different programming methodology that decouples the two in order to solve these challenges. With our approach, developers write their applications as logical monoliths, offload the decisions of how to distribute and run applications to an automated runtime, and deploy applications atomically. Our prototype implementation reduces application latency by up to 15× and reduces cost by up to 9× compared to the status quo.

---

> \[Microservices hurt] correctness. It is extremely challenging to reason about the interactions between every deployed version of every microservice. In a case study of over 100 catastrophic failures of eight widely used systems, two-thirds of failures were caused by the interactions between multiple versions of a system

> ...Running end-to-end tests with a local instance of the application becomes an engineering feat.

> When making changes that affect multiple microservices, developers cannot implement and deploy the changes atomically. They have to carefully plan how to introduce the change across 𝑛 microservices with their own release schedules.

---

> In this paper, we propose a different way of writing and deploying distributed applications, one that solves C1-C5. Our programming methodology consists of three core tenets:

> 1. Write monolithic applications that are modularized into logically distinct components.
> 2. Leverage a runtime to dynamically and automatically assign logical components to physical processes based on execution characteristics.
> 3. Deploy applications atomically, preventing different versions of an application from interacting.

The application I think I designed best followed points 1 and 3, but 2 is very interesting to me and I'd not previously considered it.

In the app I'm talking about, we horizontally scaled application servers in whole; having a way to scale the physical processes independently is a very cool idea.

---

> The key abstraction of our proposal is the component... Component method invocations turn into remote procedure calls where necessary, but remain local procedure calls if the caller and callee component are in the same process.

I really like this idea! When you're programming, you don't necessarily have to care about whether the component is a logical or physical process, just about its boundary; 

---

> While our programming model allows developers to focus on their business logic and defer a lot of the complexity of deploying their applications to a runtime, our proposal does not solve fundamental challenges of distributed systems. Application developers still need to be aware that components may fail or experience high latency.

This seems to me to wrap up a lot of the challenge of this model: it asks developers to treat calls between the boundaries of components as if they were normal local function calls, but in practice they may be distributed system calls.
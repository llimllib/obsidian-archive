[dagger.io](https://dagger.io/) launched recently

- uses Docker fundamentally, and created by the creators of Docker
	- (although tbh I'm not clear on exactly who this is or what that means?)
- uses the [[CUE language|CUE]] config language, which looks neat
- the benefits of the system are not entirely clear to me
- seems to be well-integrated with GHA, though why would I use it instead of GHA?

A pitch from the comments in news.yc:

> Each time Dagger runs your pipeline, it can produce telemetry about every aspect of your supply chain. Git SHAs, docker image checksums and cryptographic signatures, specific versions of kubernetes and cloudformation configurations, before and after templating, test results, monitoring status... It also integrates with your secrets management backends, your developer's local source code. Basically every node in your supply chain can be a node in your DAG if you want it to. The logical next step is to give you a centralized place to send all this telemetry, and tools to extract insights from it. You could also perhaps manage the configuration of your various Dagger engines in one location.

> Another product that is often requested is a _visual DAG debugger_. When a pipeline break, you want to know why, and staring at your CI logs is definitely not the best experience for that. With a web UI, there's a lot we can do there.

> The business opportunity boils down to this: if CI/CD pipelines are software, there ought to be a platform for developing that software, and an ecosystem of developers creating value around that platform. Dagger aspires to create that missing developer ecosystem. If we succeed, there will be no shortage of business opportunities. If we fail, none of the other features will matter.

-[shykes (Solomon Hykes)](https://news.ycombinator.com/reply?id=30859864&goto=item%3Fid%3D30857012%2330859864)


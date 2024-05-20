---
updated: '2024-04-23T12:01:22Z'
created: '2023-10-20T13:54:09Z'
---
[source](https://xi.zulipchat.com/#narrow/stream/197075-gpu/topic/Learning.20resources.20for.20compute.20shaders) via [toot](https://mastodon.online/@raph/109617071186970778)

Raph Levien: @Nils Martel asked on Mastodon about learning resources for GPU compute shaders. That's a deep topic, and deserves a fresh look, largely because I consider [[WebGPU]] a game changer. I'll do my best in this topic to give a fairly comprehensive answer.

Raph Levien: First, some general observations, then I'll get into specifics. Learning compute shader programming is a hard road, because there are few good resources dedicated to the topic, and it's also very much a moving target (I'll get into that more). Even so, I obviously consider it very rewarding, and am confident that computing with thousands to tens of thousands of threads will be a vital skillset for decades to come, even if (as it hopes) it evolves considerably beyond the limitations of current GPUs.

Raph Levien: The information is out there, just not in easily digestible form. To learn it, you need to read papers, technical documentation, blog posts, and above all code. Also nothing substitutes for experimentation, especially to build a mental model of performance. Your intuition of what's and fast and what's slow is _guaranteed_ to be wrong when it makes contact with real hardware. Incidentally, this is one reason I've been so obsessive about timer queries, which is sadly underdeveloped in WebGPU land. A great way to develop that intuition is to have a feedback loop of: try something, run on real hardware, measure performance, be surprised, and update your mental model so it becomes closer to what you observe on real hardware.

Raph Levien: One of the first things you'll need to do is pick a target. For learning, I personally recommend WebGPU 1.0, but it has its downsides. Another alternative I can recommend is Vulkan. I don't really recommend learning Metal (unless you're comfortable being boxed into the Apple ecosystem) or DirectX (unless you're Windows only or primarily focused on games, in which case I recommend it highly). I consider OpenCL to be pining for the fjords, and I don't believe there is any other viable alternative for compute shaders.

Raph Levien: Which brings us to CUDA. The _vast_ majority of the knowledge, documentation, and code for doing compute on GPU hardware is in CUDA. I'm not including it under the umbrella of compute _shaders_ because it requires a proprietary runtime and toolchain. There are also some important differences between the CUDA computational model and compute shaders, which it will be important to understand (it probably helps to consider an older snapshot of CUDA because most of the newer features don't exist in compute shader land). I do think any journey of learning GPU compute requires picking up at least some CUDA knowledge, and I recommend planning for that.

Raph Levien: I don't have a great list of CUDA resources handy (my own reading has been pretty disjointed), but the official [CUDA Education & Training](https://developer.nvidia.com/cuda-education-training) site is probably a good place to start. I've also enjoyed a bunch of conference talks from Nvidia engineers, topics in the [GPU Gems](https://developer.nvidia.com/gpugems/gpugems/contributors) series, and abundant code samples. I specifically want to raise up [CUB](https://nvlabs.github.io/cub/), which is a very rich set of advanced compute primitives, and [Modern GPU](https://github.com/moderngpu/moderngpu), which has a stronger pedagogical focus.

Raph Levien: Ok, let's get into what I might consider a syllabus for a class on compute shaders.

## Raph Levien: Section 1: GPU hardware and compute shader computational model

Compute shaders are a way to exploit performance from real GPU hardware, which has evolved to handle 3D graphics workloads efficiently. Those workloads are very different from standard CPU workloads in important ways: there is a huge (sometimes embarrassing) degree of parallelism, there is an intense need for memory bandwidth, but those accesses can be structured in a hierarchy (I find it useful to think of this in terms of laws of physics, how much energy it takes to move bits around on a silicon die), and there is generally a need for some but not extraordinarily intensive coordination between threads.

Raph Levien: So it is helpful to understand the basics of GPUs even before focusing too much on compute, but I'll also include compute resources here.

-   [A trip through the Graphics Pipeline 2011](https://fgiesen.wordpress.com/2011/07/09/a-trip-through-the-graphics-pipeline-2011-index/)
-   [Introduction to compute shaders](https://anteru.net/blog/2018/intro-to-compute-shaders/)
-   [WebGPU — All of the cores, none of the canvas](https://surma.dev/things/webgpu/)
-   [Compute shader 101](https://github.com/googlefonts/compute-shader-101)

Raph Levien: I also strongly recommend experimenting with ShaderToy to get a flavor for highly parallel computing. That is an extremely limited computational model compared with compute shaders, but it is still impressive how much you can do in it, and a lot of the performance advice (particularly topics such as the relative cost of memory access vs arithmetic, divergence and branches, etc) applies to compute as well. It's all running on the same hardware at the end of the day.

## Raph Levien: Section 2: Algorithmic parallelism

Some problems are "embarrassingly parallel," meaning that you can just run many different instances of the same fundamental algorithm, without requiring any coordination between them. Others (like hashing a long string) are essentially serial. The art of compute programming is the area in the middle, where the problem has inherent parallelism, but exploiting that is not immediately obvious, and some coordination between threads is needed.

Raph Levien: There is a pretty big academic literature on this. An absolute favorite is [Prefix Sums and Their Applications](https://www.cs.cmu.edu/~guyb/papers/Ble93.pdf). A lot of this academic literature assumes the [PRAM model](https://en.wikipedia.org/wiki/Parallel_RAM), which is actually not a very good model of actual GPU hardware, but is still useful for analyzing how much parallelism is available in a problem domain. I recommend [Thinking in Parallel: Some Basic Data-Parallel Algorithms and Techniques](https://users.umiacs.umd.edu/~vishkin/PUBLICATIONS/classnotes.pdf) (2010) for a solid academic treatment of this field.

Raph Levien: You still have to do a lot of work to map that to real hardware, and I'm not aware of any good writeup on that. I tried to touch on it in my [stack monoid](https://arxiv.org/abs/2205.11659) paper, but it's potentially a topic of much bigger scope. I think a fairly good _general_ piece of advice is to find a paper with an efficient parallel algorithm according to the PRAM model, then try implementing it on a real GPU. That will be a struggle, but at the end of it you'll learn a lot.

## Raph Levien: Section 3: some pedagogical compute resources

Here are some resources I found interesting, where the authors are trying to explain something. Relevance not guaranteed.

-   [WebGPU Samples: computeBoids](https://austin-eng.com/webgpu-samples/samples/computeBoids)
-   [Compute shaders: optimize your engine using compute](https://gpuopen.com/videos/optimize-your-engine-using-compute/)
-   [Vulkan guide: compute shaders](https://vkguide.dev/docs/gpudriven/compute_shaders/)
-   [Exploring ways to optimize compute shaders - Part 1](https://frguthmann.github.io/posts/compute_shaders/)
-   [Ocean waves simulation with Fast Fourier transform](https://www.youtube.com/watch?v=kGEqaX4Y4bQ) (video; [source](https://github.com/gasgiant/FFT-Ocean))
    
    [![](https://uploads.zulipusercontent.net/bbf49b6fdad688481153dccdc1927385ff7bc18e/68747470733a2f2f692e7974696d672e636f6d2f76692f6b474571615834593462512f64656661756c742e6a7067)](https://www.youtube.com/watch?v=kGEqaX4Y4bQ)
    
-   [Emulating a fake retro GPU in Vulkan compute](https://themaister.net/blog/2019/10/12/emulating-a-fake-retro-gpu-in-vulkan-compute/)
-   [Get started with compute shaders](https://community.arm.com/arm-community-blogs/b/graphics-gaming-and-vr-blog/posts/get-started-with-compute-shaders)

## Raph Levien: Section 4: some other compute shader codebases to read

-   [Vello](https://github.com/linebender/vello) of course! I plan on writing an extensive "Report on project Vello"
-   [kompute.cc](https://kompute.cc/). Focused on machine learning, and Vulkan only
-   [wonnx](https://github.com/webonnx/wonnx). Focused on machine learning, and WebGPU. In fact, the only other non-tutorial WebGPU compute codebase I'm currently aware of (I'm sure this will change rapidly)

## Raph Levien: Section 5: beyond WebGPU

WebGPU 1.0 has some serious limitations, though I believe it is a solid foundation. I think it's valuable to be aware of the ways other APIs have more powerful compute capabilities. I also believe that in time WebGPU will evolve, both by optional extensions and (hopefully) future major versions.

Raph Levien: WebGPU lacks device-scoped barriers, which mean that [single-pass prefix sum](https://research.nvidia.com/publication/2016-03_single-pass-parallel-prefix-scan-decoupled-look-back) is impossible. A good academic publication on that topic is [Inter-workgroup Barrier Synchronisation on Graphics Processing Units](https://users.soe.ucsc.edu/~tsorensen/files/phdthesis.pdf)

Raph Levien: Another major limitation is that it lacks subgroups, which are a way for blocks of threads (usually 32) smaller than a workgroup (typically 1024) to communicate with each other without going through workgroup-shared memory at all. In addition, synchronization within a subgroup is cheap or even free, as the threads within a subgroup usually execute in lock-step.

-   [Vulkan Subgroup Tutorial](https://www.khronos.org/blog/vulkan-subgroup-tutorial)
-   [Vulkan Subgroup Explained](https://www.khronos.org/assets/uploads/developers/library/2018-vulkan-devday/06-subgroups.pdf)
-   [SIMD operations in WebGPU for ML](https://www.w3.org/2020/06/machine-learning-workshop/talks/simd_operations_in_webgpu_for_ml.html)
-   [Wave Programming in D3D12 and Vulkan](https://gpuopen.com/wp-content/uploads/2017/07/GDC2017-Wave-Programming-D3D12-Vulkan.pdf)

Raph Levien: Something interesting to watch is the existence of pointers. In "basic" GPU compute (including WebGPU), there is no primitive pointer type. Instead, a memory access operation in a shader program is (generally) bound to a single buffer, and you can vary the array index within that buffer. Both CUDA and OpenCL have real pointers, which is a somewhat different programming model.

Raph Levien: However, Metal (like OpenCL) has had pointers from the beginning, and Vulkan has slowly, painfully been growing the capability. From what I've seen so far, the tooling and developer experience of pointers in Vulkan is terrible (even by Khronos standards), but it's interesting that it's there. I suspect it will end up being most useful as a compilation target from higher level languages, rather than something most programmers will use directly.

Raph Levien: Ok, I think that's about it for now. I'm sure I left out some useful resources. Others feel free to add more. It occurs to me this might be better as a wiki than a discussion thread, but we don't presently have a space for those to live. I hope Nils and others find it useful!
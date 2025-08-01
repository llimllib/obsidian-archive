---
updated: 2024-08-16T14:05:25.813Z
created: 2023-10-20T13:54:09Z
---
https://github.com/sharkdp/hyperfine

> A command-line benchmarking tool

-   Statistical analysis across multiple runs.
-   Support for arbitrary shell commands.
-   Constant feedback about the benchmark progress and current estimates.
-   Warmup runs can be executed before the actual benchmark.
-   Cache-clearing commands can be set up before each timing run.
-   Statistical outlier detection to detect interference from other programs and caching effects.
-   Export results to various formats: CSV, JSON, Markdown, AsciiDoc.
-   Parameterized benchmarks (e.g. vary the number of threads).
-   Cross-platform

Runs a command or multiple commands multiple times and reports the results

[here's an example usage](https://gist.github.com/llimllib/a98f5c185e096f6f6ec16c8172054930) where I benchmark four programs in different languages running the same regular expression
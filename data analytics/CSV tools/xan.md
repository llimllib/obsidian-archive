---
created: 2026-05-12T12:06:44.989Z
updated: 2026-05-12T12:06:44.989Z
---
https://github.com/medialab/xan

> xan is a command line tool that can be used to process CSV files directly from the shell.
> 
> It has been written in Rust to be as fast as possible, use as little memory as possible, and can very easily handle large CSV files (Gigabytes). It leverages a novel SIMD CSV parser and is also able to parallelize some computations (through multithreading) to make some tasks complete as fast as your computer can allow.
> 
> It can easily preview, filter, slice, aggregate, sort, join CSV files, and exposes a large collection of composable commands that can be chained together to perform a wide variety of typical tasks.
> 
> xan also offers its own expression language so you can perform complex tasks that cannot be done by relying on the simplest commands. This minimalistic language has been tailored for CSV data and is way faster than evaluating typical dynamically-typed languages such as Python, Lua, JavaScript etc.
> 
> Note that this tool is originally a fork of BurntSushi's xsv, but has been nearly entirely rewritten at that point, to fit SciencesPo's médialab use-cases, rooted in web data collection and analysis geared towards social sciences (you might think CSV is outdated by now, but read our love letter to the format before judging too quickly).
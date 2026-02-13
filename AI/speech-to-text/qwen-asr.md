---
created: 2026-02-12T17:54:46.745Z
updated: 2026-02-12T17:54:46.745Z
---
model: https://github.com/QwenLM/Qwen3-ASR
antirez' inference code: https://github.com/antirez/qwen-asr

> We release **Qwen3-ASR**, a family that includes two powerful all-in-one speech recognition models that support language identification and ASR for 52 languages and dialects, as well as a novel non-autoregressive speech forced-alignment model that can align text–speech pairs in 11 languages.

similar to [[voxtral.c]], antirez built a C inference harness:

> This is a C implementation of the inference pipeline for [Qwen3-ASR](https://github.com/QwenLM/Qwen3-ASR) speech-to-text models (both 0.6B and 1.7B). It has zero external dependencies beyond the C standard library and a BLAS implementation (Accelerate on macOS, OpenBLAS on Linux). Tokens stream to stdout as they are generated. The implementation runs at speed multiple of the file length even in very modest hardware, like low end Intel or AMD processor.

via [bsky](https://bsky.app/profile/antirez.bsky.social/post/3memjclbrj22v)

---
created: 2024-07-07T20:50:49.067Z
updated: 2024-07-07T20:50:49.067Z
---
https://github.com/ggerganov/whisper.cpp

> High-performance inference of [OpenAI's Whisper](https://github.com/openai/whisper) automatic speech recognition (ASR) model:

The binary produced by whisper.[[c++|cpp]] is much faster for inference than the python version [provided by openai](https://github.com/openai/whisper).

I wrapped whisper.cpp to try and provide it a nicer UI in [blisper](https://github.com/llimllib/blisper). In the process, I discovered [that the default golang bindings are very slow](https://github.com/ggerganov/whisper.cpp/discussions/312#discussioncomment-6307234), and figured out how to make them quite a bit faster.
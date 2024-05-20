---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/openai/whisper

> Whisper is a general-purpose speech recognition model. It is trained on a large dataset of diverse audio and is also a multi-task model that can perform multilingual speech recognition as well as speech translation and language identification.

an open-source model from OpenAI that turns audio into text

via [Dan Nguyen on twitter](https://twitter.com/dancow/status/1572749731704573957) 

The [new release](https://github.com/ggerganov/whisper.cpp/releases/tag/v1.4.0) has the ability to work with quantized ggml models, which makes it much easier to work with. It's quite a lot faster than the default whisper model; here's a comparison using the large-v2 model; for whisper-cpp I'm running it with `q5_0` quantization:

```
$ time whisper-cpp samples/gb0.wav /tmp/out

real	0m40.617s
user	2m43.490s
sys	0m1.806s

$ time whisper --model large-v2 --output_format=srt samples/gb0.wav
<snip output>
real	8m19.783s
user	16m23.622s
sys	9m1.749s
```

I'm using a shell script wrapper for the whisper `main` function that I wrote myself; I'd like to open source it but I'm not sure how to include the model file or tell people all the steps they need to do to generate it.

(I guess I could script all the downloading and conversion?)

To build the ggml-encoded models:

```
python convert-pt-to-ggml.py ~/.cache/whisper/large-v2.pt <whisper_repo_path> .
```

To build the quantized model, I ran:

```
$ make quantize
$ ./quantize whisper-large-v2-model.bin whisper-quantized-large-v2.ggml.q5_0.bin q5_0
```
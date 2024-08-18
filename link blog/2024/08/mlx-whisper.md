---
created: 2024-08-13T17:16:30.377Z
updated: 2024-08-18T13:30:39.554Z
---
https://pypi.org/project/mlx-whisper/

I've previously worked a bunch with [[whisper.cpp]]; today via [simon](https://simonwillison.net/2024/Aug/13/mlx-whisper/) I found out that there's an apple version.

I wanted to see how they compared performance-wise, so I tested them each against Martin Luther King's "I Have a Dream" speech.

summary: `mlx-whisper` wipes the floor with whisper.cpp in this test on my macbook pro m1 max laptop.

## testing mlx-whisper

Procedure:

- Create a virtual environment`python -mvenv .venv`
	- (I'm using python 3.12.2)
- `.venv/bin/pip install mlx-whisper`
- download the `distill-whisper-large-v3` model (1.5gb) from [here](https://huggingface.co/mlx-community/distil-whisper-large-v3/tree/main) into a folder called `model`
- transcribe the speech: `time .venv/bin/python -c "import mlx_whisper as m; print(m.transcribe('./mlk_ihaveadream_long.wav', path_or_hf_repo='./model'))"`

The transcription took 11.3 seconds

## testing whisper.cpp

- `git pull` to get the most recent version (I already had it checked out)
	- current head is `22fcd5fd`
- `make` to compile
	- I used default options, which compiles it against the Metal framework
- `time ./main --model ggml-medium.bin ./mlk_ihaveadream_long.wav`
	- the model is available [here](https://huggingface.co/ggerganov/whisper.cpp/tree/main); I already had it available locally
	- The ggml `medium` model is 1.5gb, which is why I compared it against the `distill-whisper-large-v3`. If you use ggml `large` instead, which is 3gb, the transcription goes from 35 to 59 seconds

<details>
<summary>full build flags</summary>

```
I whisper.cpp build info: 
I UNAME_S:   Darwin
I UNAME_P:   arm
I UNAME_M:   arm64
I CFLAGS:    -Iggml/include -Iggml/src -Iinclude -Isrc -Iexamples -D_XOPEN_SOURCE=600 -D_DARWIN_C_SOURCE -DNDEBUG -DGGML_USE_ACCELERATE -DGGML_USE_BLAS -DACCELERATE_NEW_LAPACK -DACCELERATE_LAPACK_ILP64 -DGGML_USE_METAL -DGGML_METAL_EMBED_LIBRARY  -std=c11   -fPIC -O3 -Wall -Wextra -Wpedantic -Wcast-qual -Wno-unused-function -Wshadow -Wstrict-prototypes -Wpointer-arith -Wmissing-prototypes -Werror=implicit-int -Werror=implicit-function-declaration -pthread -Wunreachable-code-break -Wunreachable-code-return -Wdouble-promotion 
I CXXFLAGS:  -std=c++11 -fPIC -O3 -Wall -Wextra -Wpedantic -Wcast-qual -Wno-unused-function -Wmissing-declarations -Wmissing-noreturn -pthread   -Wunreachable-code-break -Wunreachable-code-return -Wmissing-prototypes -Wextra-semi -Iggml/include -Iggml/src -Iinclude -Isrc -Iexamples -D_XOPEN_SOURCE=600 -D_DARWIN_C_SOURCE -DNDEBUG -DGGML_USE_ACCELERATE -DGGML_USE_BLAS -DACCELERATE_NEW_LAPACK -DACCELERATE_LAPACK_ILP64 -DGGML_USE_METAL -DGGML_METAL_EMBED_LIBRARY 
I NVCCFLAGS: -std=c++11 -O3 
I LDFLAGS:   -framework Accelerate -framework Foundation -framework Metal -framework MetalKit 
I CC:        Apple clang version 15.0.0 (clang-1500.3.9.4)
I CXX:       Apple clang version 15.0.0 (clang-1500.3.9.4)
```

</details>

The transcription took 35 seconds

## quality

The `mlx-whisper` transcription is of slightly higher quality than the whisper.cpp transcription

## why?

It's not clear to me how the `mlx-whisper` model can be so much faster! They are both using the GPU and similar model sizes.

I would love to hear from somebody more knowledgeable why that is.

## update

[Josh Marshall](https://x.com/josh_m/status/1824240282554208425) on twitter noted that I was comparing two different models (true!) and compared the two on more similar models, and found a smaller difference.

I downloaded the same model he used for whisper.cpp [here](https://huggingface.co/distil-whisper/distil-large-v3-ggml/tree/main) and re-ran the experiment (this time with whisper.cpp at `b91c907` and mlx-whisper at `0.3.0`, and the difference dropped to 1.78x:

```
$ hyperfine "./whisper.cpp/main -m ~/.local/share/blisper/ggml-distil-large-v3.bin mlk_ihaveadream_long.wav" $'./mlx-whisper/.venv/bin/python -c "import mlx_whisper as m; print(m.transcribe(\'./mlk_ihaveadream_long.wav\', path_or_hf_repo=\'./mlx-whisper/model\')[\'text\'])"'
Benchmark 1: ./whisper.cpp/main -m ~/.local/share/blisper/ggml-distil-large-v3.bin mlk_ihaveadream_long.wav
  Time (mean ± σ):     17.505 s ±  0.179 s    [User: 4.063 s, System: 0.867 s]
  Range (min … max):   17.080 s … 17.690 s    10 runs
 
Benchmark 2: ./mlx-whisper/.venv/bin/python -c "import mlx_whisper as m; print(m.transcribe('./mlk_ihaveadream_long.wav', path_or_hf_repo='./mlx-whisper/model')['text'])"
  Time (mean ± σ):      9.849 s ±  0.065 s    [User: 1.817 s, System: 1.635 s]
  Range (min … max):    9.806 s … 10.027 s    10 runs
 
Summary
  ./mlx-whisper/.venv/bin/python -c "import mlx_whisper as m; print(m.transcribe('./mlk_ihaveadream_long.wav', path_or_hf_repo='./mlx-whisper/model')['text'])" ran
    1.78 ± 0.02 times faster than ./whisper.cpp/main -m ~/.local/share/blisper/ggml-distil-large-v3.bin mlk_ihaveadream_long.wav
```
---
created: 2024-08-13T17:16:30.377Z
updated: 2024-08-13T17:16:30.377Z
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
- `time ./main --model ggml-large.bin ./mlk_ihaveadream_long.wav`
	- the model is available [here](https://huggingface.co/ggerganov/whisper.cpp/tree/main); I already had it available locally

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

The transcription took 59 seconds

## quality

The mlx transcription is of slightly higher quality than the whisper.cpp transcription
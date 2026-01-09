---
created: 2026-01-09T18:40:00.739Z
updated: 2026-01-09T18:40:00.739Z
---
I somehow ended up looking at whisper (an audio transcription model) stuff today, and noticed that the `turbo` models [came out since I last tested](https://github.com/openai/whisper/discussions/2363).

So I went back to my previous comparison of [[mlx-whisper]] to [[whisper.cpp]], which showed that `mlx-whisper` was **1.78x faster** and redid the test.

In the test with the models `mlx-community/whisper-large-v3-turbo` and `ggml-large-v3-turbo.bin`, `mlx_whisper` is **2.0x faster**. The `turbo` model also seems to be somewhat slower than the `distil` models are.

I tested with this bash script:

```bash
#!/usr/bin/env bash
set -euxo pipefail

# ensure whisper.cpp and mlx_whisper are up to date
pip install -U mlx_whisper
cd whisper.cpp && git pull && make && cd ..

hyperfine \
  "./whisper.cpp/main -m ~/.local/share/blisper/ggml-large-v3-turbo.bin -otxt -of /tmp/whisper_mlk.txt ./mlk_ihaveadream_long.wav" \
  "mlx_whisper --model mlx-community/whisper-large-v3-turbo -o /tmp/mlx_whisper_mlk.txt ./mlk_ihaveadream_long.wav"
```

And the results were:

```
$ hyperfine './whisper.cpp/main -m ~/.local/share/blisper/ggml-large-v3-turbo.bin -otxt -of /tmp/whisper_mlk.txt ./mlk_ihaveadream_long.wav' 'mlx_whisper --model mlx-community/whisper-large-v3-turbo -o /tmp/mlx_whisper_mlk.txt ./mlk_ihaveadream_long.wav'
Benchmark 1: ./whisper.cpp/main -m ~/.local/share/blisper/ggml-large-v3-turbo.bin -otxt -of /tmp/whisper_mlk.txt ./mlk_ihaveadream_long.wav
  Time (mean ± σ):     26.704 s ±  0.625 s    [User: 5.177 s, System: 1.228 s]
  Range (min … max):   25.902 s … 27.922 s    10 runs
 
Benchmark 2: mlx_whisper --model mlx-community/whisper-large-v3-turbo -o /tmp/mlx_whisper_mlk.txt ./mlk_ihaveadream_long.wav
  Time (mean ± σ):     13.135 s ±  0.280 s    [User: 4.465 s, System: 2.276 s]
  Range (min … max):   12.686 s … 13.663 s    10 runs
 
Summary
  mlx_whisper --model mlx-community/whisper-large-v3-turbo -o /tmp/mlx_whisper_mlk.txt ./mlk_ihaveadream_long.wav ran
    2.03 ± 0.06 times faster than ./whisper.cpp/main -m ~/.local/share/blisper/ggml-large-v3-turbo.bin -otxt -of /tmp/whisper_mlk.txt ./mlk_ihaveadream_long.wav
```
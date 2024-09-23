---
created: 2024-09-23T14:49:49.719Z
updated: 2024-09-23T14:49:49.719Z
---
It took me a while to figure out how to get gopls to recognize C headers that aren't on the system path. I finally found success by adding a `CGO_CFLAGS` environment variable to my shell, which has `-I<header path>`

For example, I have `whisper.cpp` in `~/code/tmp/whisper.cpp`, and I need to include headers from both `/include` and `/ggml/include` in that directory, so I created an environment variable:

`CGO_CFLAGS="-I/Users/llimllib/code/tmp/whisper.cpp/include -I/Users/llimllib/code/tmp/whisper.cpp/ggml/include"`
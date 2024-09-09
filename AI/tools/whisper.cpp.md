---
created: 2024-07-07T20:50:49.067Z
updated: 2024-07-07T20:50:49.067Z
---
https://github.com/ggerganov/whisper.cpp

> High-performance inference of [OpenAI's Whisper](https://github.com/openai/whisper) automatic speech recognition (ASR) model:

The binary produced by whisper.[[c++|cpp]] is much faster for inference than the python version [provided by openai](https://github.com/openai/whisper).

I wrapped whisper.cpp to try and provide it a nicer UI in [[blisper]]. In the process, I discovered [that the default golang bindings are very slow](https://github.com/ggerganov/whisper.cpp/discussions/312#discussioncomment-6307234), and figured out how to make them quite a bit faster.

---

To build the golang bindings on a mac as of version `5caa1924` (Sep 8 2024):

```
git clone github.com/ggerganov/whisper.cpp
cd whisper.cpp/bindings/go
CC=/opt/homebrew/Cellar/llvm/18.1.8/bin/clang make
```

- I needed to use `clang` from homebrew, otherwise I got: `clang: error: unsupported option '-fopenmp'`
- I get an error about `libunwind`:
```
ld: warning: reexported library with install name '/opt/homebrew/opt/llvm/lib/libunwind.1.dylib' found at '/opt/homebrew/Cellar/llvm/18.1.8/lib/libunwind.1.0.dylib' couldn't be matched with any parent library and will be linked directly
```

which [this SO answer](https://stackoverflow.com/a/78903114) suggests might be because I'm linking against system libraries instead of llvm libraries
- this patch eliminates the warning:

```
diff --git a/bindings/go/whisper.go b/bindings/go/whisper.go
index 39ec43b..464192a 100644
--- a/bindings/go/whisper.go
+++ b/bindings/go/whisper.go
@@ -10,7 +10,7 @@ import (
 
 /*
 #cgo LDFLAGS: -lwhisper -lm -lstdc++ -fopenmp
-#cgo darwin LDFLAGS: -framework Accelerate -framework Metal -framework Foundation -framework CoreGraphics
+#cgo darwin LDFLAGS: -L/opt/homebrew/opt/llvm/lib/c++ -L/opt/homebrew/opt/llvm/lib -lunwind -framework Accelerate -framework Metal -framework Foundation -framework CoreGraphics
 #include <whisper.h>
 #include <stdlib.h>
```
- though adding `LDFLAGS` as an environment variable did not succeed, presumably because it gets added to the _end_ of `LDFLAGS` instead of the beginning? I don't know.

`make test` succeeds as long as you give it the LLVM CC.
---
created: 2025-09-19T12:19:48.732Z
updated: 2025-09-19T12:19:48.732Z
---
https://garten.salat.dev/audio-in-c/hello.html

> so far, i've done my [audio dsp](https://garten.salat.dev/audio-dsp/) in JavaScript and AssemblyScript. people on the internet tell me it is not OK to use JavaScript, so I will stop now. I will do my audio coding in C from now on.

> jokes aside, here's a very simple c program:

```c
// bytebeat.c
#include <stdio.h>
int main() {
  int t = 0;
  while(1) {
    putchar(t&t>>8);
    t++;
  }
}
```

Goes on to use [[sox]] to interpret a series of C programs as sound

via [froos](https://post.lurk.org/@froos/115227479804123437) on mastodon

A followup [post](https://garten.salat.dev/audio-in-c/wasm.html) describes how to compile similar programs to [[WASM]] and run them in the browser
---
created: 2025-01-03T13:45:42.897Z
updated: 2025-01-03T13:45:42.897Z
---
https://github.com/wolfpld/vv

> With vv you can display image files directly in your terminal. This works both locally and over remote connections. An extensive range of modern image formats is supported. Image data is displayed in full color, without any color space reduction or dithering. Images are scaled to fit the available space in the terminal. Small images can be upscaled.

Unfortunately, `brew install vv` gets you [a mac vim gui](https://github.com/vv-vim/vv), so for the moment you have to download and compile it with `cmake -B build -DCMAKE_BUILD_TYPE=Release && cmake --build build`. I also had to `brew install libsixel`.
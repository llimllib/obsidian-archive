---
created: 2026-04-17T13:19:50.528Z
updated: 2026-04-17T13:19:50.528Z
---
https://github.com/arrufat/zignal
https://arrufat.github.io/zignal/

> Zignal is a zero-dependency image processing library

> - **Core Math:** Matrices (`SMatrix`, `Matrix`, SVD), PCA, ND Geometry (SIMD Points, affine/projective transforms, convex hull), Statistics, Optimization.
> - **Computer Vision:** Feature detection and matching (FAST, ORB), Edge detection (Shen-Castan), Hough Transform, Feature Distribution Matching (style transfer).
> - **Image Processing:** Spatial transforms (resize, crop, rotate), morphology, convolution filters (blur, sharpen), thresholding, advanced Color Spaces (Lab, Oklab, Oklch, Xyb, Lms, etc.), Perlin noise generation.
> - **I/O & Graphics:** Pure-Zig PNG/JPEG codecs, Canvas API (antialiasing, Bézier curves), Bitmap/PCF Fonts, Colormaps, Terminal graphics (Kitty/Sixel).
> - **Platform Support:** Native Zig, first-class Python bindings, and WASM compilation for the web.

neat-looking zig image processing library with python bindings. Has a CLI that is currently pretty bare-bones.

Pretty impressive to have a library that does its own image decoding, font rendering, etc etc!
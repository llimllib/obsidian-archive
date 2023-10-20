https://github.com/floooh/sokol

> Simple [STB-style](https://github.com/nothings/stb/blob/master/docs/stb_howto.txt) cross-platform libraries for C and C++, written in C.

STB-style means header-only library, I guess

## [](https://github.com/floooh/sokol#core-libraries)Core libraries

-   [**sokol_gfx.h**](https://github.com/floooh/sokol/blob/master/sokol_gfx.h): 3D-API wrapper (GL + Metal + D3D11)
-   [**sokol_app.h**](https://github.com/floooh/sokol/blob/master/sokol_app.h): app framework wrapper (entry + window + 3D-context + input)
-   [**sokol_time.h**](https://github.com/floooh/sokol/blob/master/sokol_time.h): time measurement
-   [**sokol_audio.h**](https://github.com/floooh/sokol/blob/master/sokol_audio.h): minimal buffer-streaming audio playback
-   [**sokol_fetch.h**](https://github.com/floooh/sokol/blob/master/sokol_fetch.h): asynchronous data streaming from HTTP and local filesystem
-   [**sokol_args.h**](https://github.com/floooh/sokol/blob/master/sokol_args.h): unified cmdline/URL arg parser for web and native apps

## [](https://github.com/floooh/sokol#utility-libraries)

## Utility libraries

-   [**sokol_imgui.h**](https://github.com/floooh/sokol/blob/master/util/sokol_imgui.h): sokol_gfx.h rendering backend for [Dear ImGui](https://github.com/ocornut/imgui)
-   [**sokol_nuklear.h**](https://github.com/floooh/sokol/blob/master/util/sokol_nuklear.h): sokol_gfx.h rendering backend for [Nuklear](https://github.com/Immediate-Mode-UI/Nuklear)
-   [**sokol_gl.h**](https://github.com/floooh/sokol/blob/master/util/sokol_gl.h): OpenGL 1.x style immediate-mode rendering API on top of sokol_gfx.h
-   [**sokol_fontstash.h**](https://github.com/floooh/sokol/blob/master/util/sokol_fontstash.h): sokol_gl.h rendering backend for [fontstash](https://github.com/memononen/fontstash)
-   [**sokol_gfx_imgui.h**](https://github.com/floooh/sokol/blob/master/util/sokol_gfx_imgui.h): debug-inspection UI for sokol_gfx.h (implemented with Dear ImGui)
-   [**sokol_debugtext.h**](https://github.com/floooh/sokol/blob/master/util/sokol_debugtext.h): a simple text renderer using vintage home computer fonts
-   [**sokol_memtrack.h**](https://github.com/floooh/sokol/blob/master/util/sokol_memtrack.h): easily track memory allocations in sokol headers
-   [**sokol_shape.h**](https://github.com/floooh/sokol/blob/master/util/sokol_shape.h): generate simple shapes and plug them into sokol-gfx resource creation structs
-   [**sokol_color.h**](https://github.com/floooh/sokol/blob/master/util/sokol_color.h): X11 style color constants and functions for creating sg_color objects

Found it via this very neat-looking mini golf game, written in C and utilizing several high leverage libraries such as this: https://github.com/mgerdes/Open-Golf

introductory blog post: https://floooh.github.io/2017/07/29/sokol-gfx-tour.html
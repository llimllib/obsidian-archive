---
created: 2024-09-23T12:52:40.100Z
updated: 2024-09-23T12:52:40.100Z
---
I wanted to compile a file from the ffmpeg [examples directory](https://github.com/FFmpeg/FFmpeg/tree/n7.0.2/doc/examples), since I'm considering writing golang that links directly to ffmpeg via cgo.

I don't use C often enough to remember how everything works, so I have to re-figure-out how to compile stuff every time. Here's what I ended up with:

```
clang \
  -I/opt/homebrew/Cellar/ffmpeg/7.0.2/include \
  -L/opt/homebrew/Cellar/ffmpeg/7.0.2/lib/ \
  -lavutil -lavfilter -lavformat \
  decode_filter_video.c
```

- `-I`: tells clang to search the given directory for header files
	- You can use the `C_INCLUDE_PATH` environment variable instead if you prefer
- `-L`: tells clang to search the given directory for objects to link
	- You can use the `LIBRARY_PATH` environment variable instead
		- The difference between `LIBRARY_PATH` and `LD_LIBRARY_PATH` is that the latter is used at runtime for loading dynamic libraries
- `-l<libname>`: tells clang to link the library given by `<libname>`
	- I had to just kind of guess at which ones of these I needed to resolve all the undefined symbols errors I was getting
	- Is there a way to have the computer figure out which libraries you need, or is it just required for the programmer to know which `-l<whatever>` flags need to be included?

## clangd

Without any [configuration](https://clangd.llvm.org/config), clangd won't be able to find the header files you need. Here's a config file I created to give it the header directory and add `-Wall`. Save it to `.clangd`:

```
CompileFlags:
  Add:
    - "-Wall"
    - "-I/opt/homebrew/Cellar/ffmpeg/7.0.2/include"
```
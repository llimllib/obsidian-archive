1. `brew install emscripten`
2. clone sqlite: `https://github.com/sqlite/sqlite.git`
3. `cd sqlite`
4. `./configure` (to build the wasm version, you'll need to have built a makefile first)
5. `make fiddle`
6. Once that completes, you should have the wasm version of sqlite built, as well as the fiddle (available [here](https://sqlite.org/fiddle/index.html)). To run it, I went to `ext/wasm/fiddle` and ran [[devd]] with `devd -ol .`

Now what I'd like to figure out is how to build that with extensions, or how to enable javascript extensions like in `sql.js`

The functions I want are available in [sqlean/stats](https://github.com/nalgeon/sqlean/blob/main/docs/stats.md), let's figure out how to compile it:

1. `make prepare-dist`
2. `make download-sqlite SQLITE_VERSION="3360000" SQLITE_RELEASE_YEAR=2021`
3. `make download-external SQLITE_BRANCH=3.36`
	1. I stole those values from [here](https://github.com/nalgeon/sqlean/blob/main/.github/workflows/build.yml#L15)
4. `make compile-macos-arm64` 
	1. now there's `dist/arm64/stats.dylib` et al

How [sqlite-lines](https://github.com/asg017/sqlite-lines) builds his sqlite-wasm-with-extensions is by including the sqlite amalgamation.

Of course, this is a yak-shave! So we need to get a particular version of emcc running in order to compile their code. Let's try using [this page](https://emscripten.org/docs/getting_started/downloads.html) and see if we can't get version 3.1.5 installed. (Homebrew currently has 3.1.20 which [throws an error](https://github.com/asg017/sqlite-lines/issues/13))

1. `git clone https://github.com/emscripten-core/emsdk.git && cd emsdk`
2. `./emsdk install 3.1.5`
	1. that ran and succeeded and installed the tools to `./upstream/emscripten/` and `./node`
3. `source ./emsdk_env.sh`
	1. this adds the directories above to the path
4. et voila
```
$ emcc --version
emcc (Emscripten gcc/clang-like replacement + linker emulating GNU ld) 3.1.5 (d33328b22db1aa62a51c50731e9645951a2038bc)
```
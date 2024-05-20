---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---

I'm trying to package [whisper.cpp](https://github.com/ggerganov/whisper.cpp#blas-cpu-support-via-openblas) as a library for homebrew

- [Formula cookbook](https://docs.brew.sh/Formula-Cookbook)
- [Adding software to homebrew](https://docs.brew.sh/Adding-Software-to-Homebrew)

- `brew create --autotools https://github.com/ggerganov/whisper.cpp/archive/refs/tags/v1.4.0.tar.gz`
	- created the package as `lib-whispercpp`, I'm not sure if that's because of something I did earlier or if it auto-decided that's what the package name should have been
	- Later on, I changed it to `libwhisper` because that seems to be the best match for their naming conventions
- I found it helpful to clone [homebrew-core](https://github.com/Homebrew/homebrew-core) so I could run greps against the already-existing formulae and search for useful tips and tricks
- I made a directory and created a very short makefile to save commands I used frequently:

```makefile
.PHONY: edit
edit:
	nvim /opt/homebrew/Library/Taps/homebrew/homebrew-core/Formula/libwhisper.rb

.PHONY: audit
audit:
	brew audit --new libwhisper

.PHONY: install
install:
	brew install --build-from-source libwhisper

.PHONY: install
uninstall:
	- brew uninstall libwhisper

.PHONY: test
test:
	# I ended up writing a small C program to use both as the test in the
	# formula, as well as to test the installed library
	/usr/bin/clang test.c -I/opt/homebrew/Cellar/libwhisper/1.4.0/include -L/opt/homebrew/Cellar/libwhisper/1.4.0/lib -lwhisper -o test
	./test
	brew test libwhisper
```

I wanted to create a tap so that I could install in the meantime. for use in [blisper](https://github.com/llimllib/blisper) (and maybe other experiments), so I:

- created a repository: `gh repo create --public llimllib/homebrew-whisper`
	- [link](https://github.com/llimllib/homebrew-whisper)
- added it as a remote: `git remote add origin https://github.com/llimllib/homebrew-whisper.git`
	- (I had forgotten the `--src` arg to `gh repo create`
- pushed a `Formula` directory containing the formula I'd just built, a README, and a few gitihub actions I took from `brew tap-new llimllib/deleteme`
	- I didn't expect that latter command to install into the brew directory, but it did; I went in it to inspect and copy their template files then deleted it after
- To test the repo, I uninstalled `libwhisper` that I had done locally, and ran:
	- `brew install llimllib/whisper/libwhisper`
	- which worked! neato.
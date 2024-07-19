---
updated: '2024-02-29T19:14:55Z'
created: '2024-02-27T19:40:00Z'
---
[[Homebrew]] is a package manager which a lot of people use, and as software that a lot of people use, a lot of people like to complain about.

I'm not here to tell you not to complain about it, but I _do_ want to share why I love homebrew, and how you might grow to - if not love it - at least find it a part of a productive workflow.
## My One Iron Rule of Homebrew

**Don't rely on the particular version of something installed via homebrew**

Homebrew, in my workflow, has one job: install command line software and keep it up to date. For quite a lot of software, the only thing I care about is "is it up to date" - and this is the software that I install with homebrew.

For example, I use `ffmpeg` on the command line semi-regularly. `ffmpeg` has a bunch of dependencies and is generally kind of a pain in the ass to install and keep up to date on its own.

But with homebrew, I just `brew install ffmpeg`, and if I need to update it, 💥 `brew upgrade ffmpeg` gets me the newer version. This works great!

## Homebrew owns the things it installs

The most common case I see where people get frustrated is when they do something like `brew install python`, and then start relying on the python version they've just installed for running their own scripts.

In my mental model, when I say `brew install python`, I am telling homebrew _"go ahead and install a version of python for yourself"_, rather than _"install a version of python for me"_.

Later on, if I were to update some package in homebrew that depends on some other package in homebrew, it **would** update my python version without telling me, and if I'm depending on that python version, I would be upset because it would either cease to exist or become a broken shell until it gets cleaned up.

**When I install a package with homebrew, homebrew owns it and may upgrade it at any time**

## I use asdf for versions I want to control manually

If I care about the particular version of a program, such as a programming language environment or a database server, I install it myself, either manually or with a tool such as [[asdf]].

When I `asdf install python 3.12.1`, I have a good mental model of what happens: python version 3.12.1 is downloaded and installed by [pyenv](https://github.com/pyenv/pyenv/) to my asdf directory. At that point, I can be confident that version 3.12.1 is going to be available from now until such time as I take some action to uninstall it.

`asdf` has plugins for most software, and some newer software such as rust can handle this version juggling for me. Here's a brief list of how I install some of the programming environments I care about:

- go: [asdf-golang](https://github.com/asdf-community/asdf-golang) 
	- and possibly [gotip](https://pkg.go.dev/golang.org/dl/gotip) if I need development versions
- javascript: [asdf-nodejs](https://github.com/asdf-vm/asdf-nodejs)
- postgres: [asdf-postgres](https://github.com/smashedtoatoms/asdf-postgres)
- python: [asdf-python](https://github.com/asdf-community/asdf-python)
- ruby: [asdf-ruby](https://github.com/asdf-vm/asdf-ruby)
- rust: use [rustup](https://rustup.rs/)
- terraform: [asdf-hashicorp](https://github.com/asdf-community/asdf-hashicorp)

(update: as per several commenters (thanks!) I'm now giving [[mise]] a try)

## Custom taps are generally reliable

Some software, such as `mongodb`, provides [custom taps for installation](https://github.com/mongodb/homebrew-brew).

In my experience, these have been reliable, and I break my "iron rule" for mongo by installing `mongodb/brew/mongodb-community@<version>` when I need to run mongo.

But that's not as catchy I suppose.

## Why do I love homebrew

If it seems like I've laid out a bunch of exceptions and rules to follow to avoid problems, why do I actually like it?

- For software that I just want to stay up to date, which is quite a lot of the software I use at the CLI, homebrew does a great job of keeping it up to date
- homebrew's coverage of modern software releases is extensive
- package versions update nearly immediately, so if I need an updated version of something I rarely have to wait
- many complex package installations are boiled down into `brew install <package>`
	- An example: `gdal` is a giant pain to install otherwise
- it can install and keep GUI programs up to date
- creating your own recipes is very simple; see next section

## Creating your own custom tap is extremely simple

If I have some software that I'd like to create a recipe for and allow other people to install via homebrew, it's reasonably easy to do. 

My github username is `llimllib`, and an example piece of software I wrote is [blisper](https://github.com/llimllib/blisper), which is a CLI and wrapper I wrote around [whisper.cpp](https://github.com/ggerganov/whisper.cpp). Here's how I made it installable via homebrew:

- Created a repository [`homebrew-whisper`](https://github.com/llimllib/homebrew-whisper/)
- Added a `Formula` directory with a pair of [formulas](https://docs.brew.sh/Formula-Cookbook) in it
	- each is [short, declarative, and simple](https://github.com/llimllib/homebrew-whisper/blob/main/Formula/blisper.rb)

After that, I can just tell people to run `brew install llimllib/whisper/blisper` and they should be up and running with my software.
## Simplicity

Why I love homebrew is wrapped up in how simple that process is; it isn't fit for everything, but it is simple enough that if you invest a bit of energy into understanding how it works, you can easily comprehend it well.

It's an incomplete package manager that doesn't try to solve every problem - particularly it's uninterested in letting you run a particular version of any given software - but it's very good at solving the problem of installing the most recent version of CLI tools.

I have found the pairing of `homebrew` and `asdf` to satisfy my needs as somebody that hacks on a lot of different software in a lot of different ecosystems, and I hope sharing my process and a bit of my mental model might help you figure out something that works well for you.

If you have comments to make, I'm on [mastodon](https://hachyderm.io/@llimllib/112005194762232755) and happy to talk about how I use homebrew and asdf, and manage my computer generally.
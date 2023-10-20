Some notes on how I use [asdf](https://asdf-vm.com/) to install and manage programming language environments. I've been using it for a while now and I'm very happy with it - read their [getting started](https://asdf-vm.com/guide/getting-started.html) page to get it installed.

Pairs well with [[direnv]] for managing project-specific environments.

List every installed env: `asdf list`

List installed pythons: `asdf list python`

List all available pythons: `asdf list all python`

Install a recent pypy: `asdf install python pypy3.9-7.3.9`

Update a plugin: `asdf plugin update ruby`

Update asdf itself: `asdf update`

Make a recent pypy the locally active pypy (writes a `.tool-versions` file):

```shell
$ asdf local python pypy3.9-7.3.9
$ cat .tool-versions
python pypy3.9-7.3.9
```

Where's `pip` currently coming from?

```shell
$ which pip
/Users/llimllib/.asdf/shims/pip
```

It's a shim inserted by asdf to run pip with the current local version.

How long does my notes generator take under pypy?

```shell
# `python` here is pypy
$ python --version
Python 3.9.12 (05fbe3aa5b0845e6c37239768aa455451aa5faba, Mar 29 2022, 09:54:47)
[PyPy 7.3.9 with GCC Apple LLVM 13.0.0 (clang-1300.0.29.30)]

$ time python run.py
unable to find link "player", "fg_pct" in pandas
unable to find link "player", "fg_pct" in pandas
Unable to find page "player", "fg_pct"
Unable to find page "player", "fg_pct"
Unable to find page Change_DistillingTree_Differencing_for_Fine-Graine.pdf
Unable to find page gumtree.pdf

real	0m8.564s
user	0m8.044s
sys	0m0.468s
```

And, how long does it run under python? Let's switch to python 3.10.0 and try it

```shell
$ asdf local python 3.10.0

# you can see the changes in `.tool-versions`:
$ cat .tool-versions
python 3.10.0

# and check the python version:
$ python --version
Python 3.10.0

$ time python run.py
unable to find link "player", "fg_pct" in pandas
unable to find link "player", "fg_pct" in pandas
Unable to find page "player", "fg_pct"
Unable to find page "player", "fg_pct"
Unable to find page Change_DistillingTree_Differencing_for_Fine-Graine.pdf
Unable to find page gumtree.pdf

real	0m9.430s
user	0m9.024s
sys	0m0.260s
```

I switched to an even older version to see if it would be slower, but the type annotations sadly aren't compatible. Computers.

A key command is `asdf reshim`; if you install new binaries via your programming environment's package manager (`gem`, `pip`, `npm`, etc), you should run `asdf reshim` or it may not pick up the binary you installed.

If you don't, you may see an error like this one I saw when running my notes generator:

```
No preset version installed for command pygmentize
Please install a version by running one of the following:

asdf install python pypy3.9-7.3.9

or add one of the following versions in your config file at /Users/llimllib/code/obshtml/.tool-versions
python 3.10.0
```

What happened was that I `pip install`ed the binary `pygmentize`, but `asdf` doesn't know to insert a `shim` for it in this version of python until I run `asdf reshim`. After I did, everything worked as expected.

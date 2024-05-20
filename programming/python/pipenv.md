---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://pipenv.pypa.io/en/latest/

Install is a bit wonky, they want you to do a user installation:

`pip install --user pipenv`

Which installs `pipenv` into a `bin` directory inside [`site.USER_BASE`](https://docs.python.org/3/library/site.html#site.USER_BASE) which for me is `$HOME/.local`; if you're unsure what yours is you can do `python -c "import site; print(site.USER_BASE)"`. To access it, I had to add `$HOME/.local/bin` to my `$PATH` variable, since I had never used anything in that directory before.

> Side note: from my normal [[asdf]]-installed python, I get `~/.local` as the user base; if I call the python command above from inside a pipenv-activated shell, I get `~/Library/Python/3.10`, despite that fact that both pythons are the same. I don't understand why

Once it is installed, you can do `pipenv install <package>`, and it will add it to a file called `Pipfile`, and store a lock file in `Pipfile.lock`. If you're familiar with bundler or npm, these should be familiar to you.

Here's what the first Pipfile I made, after `pipenv install nba_api pandas pyarrow fastparquet`:

```toml
[[source]]
url = "https://pypi.org/simple"
verify_ssl = true
name = "pypi"

[packages]
nba-api = "*"
pandas = "*"
pyarrow = "*"
fastparquet = "*"

[dev-packages]

[requires]
python_version = "3.10"
```

It has a bit of metadata, then specifies the packages I have installed, and the version of python it requires.

By default, pipenv stores your packages in a virtualenv it creates in `{site.USER_BASE}/share/virtualenvs/{directory_name}-{hash}`; for me in this case it is stored in `~/.local/share/virtualenvs/test_nba_api-xg-_2li1`.

That name is not stored in the Pipfile, so if you were to move your code or rename the directory it's in, you would lose access to the virtualenv that Pipenv created.

You can set the `PIPENV_VENV_IN_PROJECT` environment variable to 1 to have pipenv use a `.venv` directory in your project instead ([docs](https://pipenv-fork.readthedocs.io/en/latest/advanced.html#custom-virtual-environment-location)); I set this variable in [my .zshrc](https://github.com/llimllib/personal_code/blob/336d0220c714fc01798d372331222cf34802592d/homedir/.zshrc#L285-L288) 

> side note: I'm not sure why they don't just store that metadata in the Pipfile!

If you don't want that, you can set an environment variable `PIPENV_VENV_IN_PROJECT=1`, in which case it will store the virtualenv in a directory called `.venv` in the directory you do your first `pipenv install` from.

## Commands

- `pipenv install` without packages will install everything specified in your `Pipfile.lock`
- `pipenv install <package>` will install `<package>` to your virtualenv and add it to your `Pipfile` and store the exact version in `Pipfile.lock`
- `pipenv install --dev <package` to install a development package
- `pipenv shell` will activate the virtualenv that pipenv created in your current shell; when you're done with it you can run `deactivate` like normal
- If you don't want to use `pipenv shell`, you can use `pipenv run`, which functions much like `bundle exec`
- `pipenv scripts` works much like `npm run` - [documentation](https://pipenv.pypa.io/en/latest/advanced/#custom-script-shortcuts)
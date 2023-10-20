To get [[pyright]] to use a virtualenv named `.venv` in your project's directory:

- Create a file named `pyproject.toml` (if one doesn't already exist) and add the following configuration section:
```toml
[tool.pyright]
venvPath='.'
venv=".venv"
exclude=['.venv']
```

- That's it! now if you relaunch pyright or your editor, it should pick up libraries in your venv

[Here's a list of configuration variables you can use](https://github.com/microsoft/pyright/blob/bffc50a59d893be79d5045bd215d738547e2e83e/docs/configuration.md) in that section
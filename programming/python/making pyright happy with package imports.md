by default, pyright will not recognize package imports because it doesn't know where your project root is. To fix that, create a `pyproject.toml` file at your project root.

I _think_ you don't actually need any options in that case, but I created it with just this config:

```toml
[tool.pyright]
include = ["src"]
```

and it began recognizing my package imports so I got my intellisense (which I have allowed myself to become dependent on... sigh...)
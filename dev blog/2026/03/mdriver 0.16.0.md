---
created: 2026-03-14T01:39:04.440Z
updated: 2026-03-14T01:39:04.440Z
---
While working with [[pr-review]], I found a bug with how [[mdriver]] was parsing fenced code blocks.

<details><summary>what is mdriver?</summary>

`mdriver` is a streaming markdown renderer written in rust, ideal for displaying LLM output in your terminal with syntax highlighting, terminal hyperlinks, and generally attractive display.

</details>

If they followed directly after text, for example if my PR review bot told me:

````markdown
your code is not even syntactically valid python
```python
for score in seven years ago:
```
````

it was failing to display the code block properly.

Release [0.16.0](https://github.com/llimllib/mdriver/releases/tag/v0.16.0) fixes this bug.

You can install `mdriver` with brew (`brew install llimllib/tap/mdriver`) or cargo (`cargo install mdriver`)
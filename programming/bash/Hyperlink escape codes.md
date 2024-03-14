To print out a clickable hyperlink in a [terminal that supports] the [OSC8 escape code](https://gist.github.com/egmontkob/eb114294efbcd5adb1944c9f3cb5feda), use:

```bash
printf '\e]8;;http://example.com\e\\This is a link\e]8;;\e\\\n'
```

Found via trying to get the [[gh]] cli to output nicer code search results that I can get more context from

Here's a python function that returns an appropriately escaped hyperlink ready for display in the terminal:

```python
import urllib.parse

def link(url, link):
    return f'\033]8;;{urllib.parse.quote(url)}\033\\{link}\033]8;;\033\\'
```

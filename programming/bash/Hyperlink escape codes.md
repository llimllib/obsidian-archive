---
updated: 2024-09-04T19:36:10.190Z
created: 2024-03-13T15:50:41Z
---
To print out a clickable hyperlink in a [terminal that supports] the [OSC8 escape code](https://gist.github.com/egmontkob/eb114294efbcd5adb1944c9f3cb5feda), using bash:

```bash
printf '\e]8;;http://example.com\e\\This is a link\e]8;;\e\\\n'
```

The structure of that URL is (keep in mind that `\e` represents the same thing as `\x1b`):

```
OSC8 := \x1b]8;;
ST := \x1b\x5C
{OSC8}{url}{ST}{link text}{OSC8}{ST}
```

- that's a bit simplified, as there can be parameters between the `;;` in OSC8, but it mostly gets the job done. See [the spec](https://gist.github.com/egmontkob/eb114294efbcd5adb1944c9f3cb5feda) for more info.

Found via trying to get the [[gh]] cli to output nicer code search results that I can get more context from

Here's a python function that returns an appropriately escaped hyperlink ready for display in the terminal:

```python
def link(url, link):
    return f'\033]8;;{url}\033\\{link}\033]8;;\033\\'
```

note that this assumes your URL is properly URL-escaped.

Javascript code to output an OSC8 link:

```javascript
function link(url, text) {
  const osc8 = '\x1b]8;;';
  const st = '\x1b\x5C';
  return `${osc8}${url}${st}${text}${osc8}${st}`;
}
```

Unfortunately the `ansi-regex` package [has an issue](https://github.com/chalk/ansi-regex/issues/56) where it doesn't support the standard `ST` (string termination) sequence of `\x1b\x5C`; I've submitted a [pull request](https://github.com/chalk/ansi-regex/pull/58) and we'll see if it gets in.
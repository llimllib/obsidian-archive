---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/curl/trurl

I have long complained about the lack of a standard unix tool for manipulating URLs at the command line; now there's one from Daniel Stenberg, the author of curl.

introduced here: https://daniel.haxx.se/blog/2023/04/03/introducing-trurl/

see also [[parse-url]]

```
$ ./trurl https://usps.gov --json
{
  "url": "https://usps.gov/",
  "scheme": "https",
  "host": "usps.gov",
  "port": "443",
  "path": "/",
}
```

Not yet available on homebrew, but building it was trivial; clone the repo and `make`
---
created: 2024-07-03T18:01:50.200Z
updated: 2024-07-03T18:01:50.200Z
---
https://github.com/h4l/json.bash

> `json.bash` is a command-line tool and bash library that creates JSON.

```sh
$ jb name=json.bash creates=JSON dependencies:[,]=Bash,Grep
{"name":"json.bash","creates":"JSON","dependencies":["Bash","Grep"]}
```

> `json.bash`'s _[one thing](https://en.wikipedia.org/wiki/Unix_philosophy)_ is to get shell-native data (environment variables, files, program output) to somewhere else, using JSON encapsulate it robustly.

> Creating JSON from the command line or a shell script can be useful when:

> - You need some ad-hoc JSON to interact with a JSON-consuming application
> - You need to bundle up some data to share or move elsewhere. JSON can a good alternative to base64-encoding or a file archive.
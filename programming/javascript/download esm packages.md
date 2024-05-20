---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://simonwillison.net/2023/May/2/download-esm/

Simonw, via mbostock, had the neat idea to write a script to download ESM packages from npm and rewrite them to use relative imports, which allows you to import them as modules without running a compile step on your JS.

https://github.com/simonw/download-esm

It's very simple; and hrbrmstr rewrote it in go:

https://github.com/hrbrmstr/esmdl

read the code to see how it just downloads the code and uses a few regexes to rewrite the imports. Clever.
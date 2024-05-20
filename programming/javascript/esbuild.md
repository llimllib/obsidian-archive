---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
Simplest possible usage of esbuild: https://gist.github.com/llimllib/6730d9d01011e4031b2f1190740d9ad4

I rewrote it as a blog entry here: https://billmill.org/bundle_d3_with_esbuild.html

Command to build a library composed of typescript files into a single library importable as an IIFE, with a given name. In this case, I'm building `chessops` into a javascript library that can be imported, giving a global name of `chessops` to the imports:

`esbuild --bundle --outdir=build --global-name=chessops ./src/index.js`
Simon [asks](https://til.simonwillison.net/javascript/jsr-esbuild) for the simplest way to package a deno package from [jsr](https://jsr.io/) for the browser. Here's what I did:

## create a package

```bash
# create a package
mkdir deno-esbuild && cd deno-esbuild && npm init -y

# install yassify
npx jsr add @kwhinnery/yassify

# install esbuild
npm add --save-dev esbuild

# create a test.js file
cat <<EOF > test.js
import * as mod from "@kwhinnery/yassify";

addEventListener("DOMContentLoaded", (_) => {
  const h1 = document.querySelector("h1");
  h1.innerText = mod.yassify(h1.innerText);
});
EOF

# compile it with esbuild
npx esbuild test.js --bundle > bundle.js

# create an html file
printf "<script src="bundle.js"></script><h1>hi simon</h1>" >| index.html
```

Now, open the HTML file and you should see something like:

![[Pasted image 20240302154626.png]]
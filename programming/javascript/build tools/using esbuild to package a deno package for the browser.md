Simon [asks](https://til.simonwillison.net/javascript/jsr-esbuild) for the simplest way to package a deno package from [jsr](https://jsr.io/) for the browser. Here's what I did:

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
printf '<script src="bundle.js"></script><h1>hi simon</h1>' > index.html
```

Now, open the HTML file and you should see something like:

![[Pasted image 20240302154626.png]]

## part 2: using datasette/table

The simplest way I found to bundle a file using the JSR version of `datasette/table` is to use deno, and use a URL import instead of a prefixed `jsr:` import.

```bash
mkdir deno-datasette && cd deno-datasette && deno init
```

Create a `test.js` file that looks like:

```js
import * as mod from "https://jsr.io/@datasette/table/0.1.0/datasette-table.js";
console.log(mod);
```

Create a `bundle.js` file that looks like this:

```js
import * as esbuild from "https://deno.land/x/esbuild@v0.19.11/mod.js";
import { denoPlugins } from "https://deno.land/x/esbuild_deno_loader@0.8.5/mod.ts";

const result = await esbuild.build({
  plugins: [
    ...denoPlugins({
      configPath: await Deno.realPath("deno.json"),
    }),
  ],
  entryPoints: ["./test.js"],
  outfile: "./bundle.js",
  bundle: true,
  format: "esm",
});

console.log(result.outputFiles);

esbuild.stop();
```

This file uses the [esbuild deno loader](https://github.com/lucacasonato/esbuild_deno_loader/tree/main) plugin from github. Now you can build a bundle:

```bash
deno run --allow-read --allow-env --allow-run build.js
```

Then you can create an HTML file that looks like this:

```html
<script src="bundle.js"></script>
<datasette-table
  url="https://global-power-plants.datasettes.com/global-power-plants/global-power-plants.json"
></datasette-table>
```

And if you run it, you will see a web page showing a datasette table:

![[Pasted image 20240302161812.png]]
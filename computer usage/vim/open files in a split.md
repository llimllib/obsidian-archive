`vim -o index.js index.html`

to open them vertically:

`vim -O index.js index.html`

You can pass a number if you want to only open a certain number of splits.

`vim -O2 index.js util.js index.html` will open the js files in vertical splits, and index.html as a buffer but won't make a split for it.

This is a thing that I seem to want to do at exactly the frequency where I look up how to do it one time and have forgotten it by the next.
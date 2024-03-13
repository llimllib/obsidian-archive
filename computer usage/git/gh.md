https://cli.github.com
https://github.com/cli/cli

I've begun relying on this tool when interacting with github, especially as it handles auth in nicer ways than google.

To set an alias: `gh alias set clone 'repo clone'` (I forget the `repo` part of that 100% of the time)

----

`gh run watch` is a handy command, it will give you a list of the actions currently running and let you watch it in the terminal until it's complete.

Ned Batchelder wasn't satisfied with that tool, so he created [watchgha](https://github.com/nedbat/watchgha). The main benefit is that it shows you all the workflows associated with a PR instead of just one. Here's the two running side by side, `gh run watch` on the left and `watchgha` on the right:

![[Pasted image 20230725102917.png]]

You get a denser display with `watch_gha`

---

Code search is great: `gh search code "parquet-wasm" "writeParquet" --language=typescript` will search all of github for examples of code using `parquet-wasm` and `writeParquet`, and print them to your console.

Unfortunately, they don't give you enough context to see what's going on, and they also don't give you a link to view the code on github, or any way to view it with more context in the console.

I messed around a bit with the gh cli's template support (see `gh help formatting`) to get to this, which does a neat terminal escape trick to make the displayed path a [[Hyperlink escape codes|hyperlink]] (took me a bit to find that it's [implemented here](https://github.com/cli/go-gh/blob/45fa8a46ae55cf5975cc2bd891b46ffc3d50e4f6/pkg/template/template.go#L254-L261)) to view the code on github:

```shell
gh search code --json path,repository,sha,textMatches,url -t '{{range .}}
{{ printf "%s" .repository.nameWithOwner | autocolor "blue"}} {{ hyperlink .url (printf "%s" .path | autocolor "green") }}
{{ range .textMatches }}
    {{ .fragment }}
{{end}}
{{end}}' "parquet-wasm" "writeParquet" --language=typescript
```

One downside of this is that you lose the nice coloring of the matches that the gh cli provides natively, and you can't easily get it back inside the template.

I played around with using [[jq]] to filter the input, and ended up with this monstrous expression which highlights the matches within a single code search result:

```shell
cat /tmp/oneresult.json | 'foreach (.matches | map(.text) | unique[]) as $match (.fragment; sub($match; "\u001b[1;31m"+$match+"\u001b[0m"; "g"))'
```

But I failed at figuring out how to do that for each match in the result, which would allow me to use the jq filter option to the `gh` cli to pre-highlight the matches, which would print them nicely with the template.

Perhaps I should just write a program to print them out exactly as I want to.
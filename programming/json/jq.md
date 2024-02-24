https://stedolan.github.io/jq/

Great tool for filtering, formatting, and outputting json.

A bit cryptic though.

- The manual is complete but not very thorough: https://stedolan.github.io/jq/manual/
- There's a lot more information on the wiki: https://github.com/stedolan/jq/wiki/jq-Language-Description
- Good intro article: https://earthly.dev/blog/jq-select/
- I like that article better than the bit I wrote for work: https://gist.github.com/llimllib/84a4345e87c5bc0758597c2052cbc680

`jq` appears to be largely unmaintained at this point, which is sad
- update: [[jq is alive again]]!

- convert json to csv, something I modified from stack overflow:

```
cat some.json | jq -r '(map(keys) | add | unique) as $cols | map(. as $row | $cols | map($row[.])) as $rows | $cols, $rows[] | @csv'
```

[JBOL](https://github.com/fadado/JBOL#-jbol-) is a collection of jq modules you can install. [this is an example](https://github.com/fadado/JBOL/blob/master/fadado.github.io/array/array.jq) of some of the powerful stuff you can do with jq, I understand very little of it

---

Find every package.json file in a monorepo (using [[fd]]), and update the react version in dependencies or in peerDependencies, if it exists:

```bash
#!/usr/bin/env bash
# update react in all package.json files
#
# To install dependencies on a mac:
# brew install fd jq sponge

dep='if .dependencies.react != null then .dependencies.react = "^18.2.0" else . end'
depDom='if .dependencies."react-dom" != null then .dependencies."react-dom" = "^18.2.0" else . end'
peerDep='if .peerDependencies.react != null then .peerDependencies.react = "18.x" else . end'
peerDepDom='if .peerDependencies."react-dom" != null then .peerDependencies."react-dom" = "18.x" else . end'

for p in $(fd package.json --exclude bower_components); do
    jq "$dep" "$p" | 
        jq "$depDom" | 
        jq "$peerDep" | 
        jq "$peerDepDom" | 
        sponge "$p"
done
```

---

Turn a folder full of json files, each of which contains an array of objects, into a single array of objects, and output it to a file:

```console
jq -n '[inputs.[]]' lists/*.json > one_big_list.json
```

uses the [inputs](https://jqlang.github.io/jq/manual/v1.7/#inputs) special variable
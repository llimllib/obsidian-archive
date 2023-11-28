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
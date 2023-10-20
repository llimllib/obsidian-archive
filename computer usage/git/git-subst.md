https://github.com/dspinellis/git-subst

> Git plugin for substituting a regular expression with some text across all files under revision control

I especially like that they added the `-n` option to do a dry run. Code is [appropriately clean and simple](https://github.com/dspinellis/git-subst/blob/main/git-subst)

```
Examples:
  git subst old new
  git subst '\.Body' .body  # . RE character is escaped
  git subst '\<statuscode\>' statusCode  # Matches whole words only
  git subst '\.custom\(([^)]*)\)' '.\1'  # .custom(foo) becomes .foo
```

via [the author's toot](https://elk.pwm.social/hachyderm.io/@CoolSWEng@mastodon.acm.org/110459031970338816)
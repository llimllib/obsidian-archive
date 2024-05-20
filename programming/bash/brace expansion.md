---
updated: '2024-02-20T14:21:00Z'
created: '2024-02-20T14:21:00Z'
---
https://matttproud.com/blog/posts/tip-shell-brace-expansion.html
https://www.gnu.org/software/bash/manual/html_node/Brace-Expansion.html

`brace expansion` is the name for the bash syntax often used for something like listing what files to prettify:

`prettier *.{js,jsx,ts}`

the article above gives some neat usages of it, I especially hadn't considered that you can use it to make a cartesian product of expansions:

```
$ echo {a,b,c}{1,2,3}{α,β,γ}
a1α a1β a1γ a2α a2β a2γ a3α a3β a3γ b1α b1β b1γ b2α b2β b2γ b3α b3β b3γ c1α c1β c1γ c2α c2β c2γ c3α c3β c3γ
```

You can use a variable in a brace expansion:

```
$ ext=md; ls *.{$ext,js}
CHANGELOG.md       README.md          babel.config.js    jest.config.js     migrate.js*        postcss.config.js  tracing.js
```

as far as I know, however, you can't do brace expansion on an array, which is unfortunate. I'd love to be able to say:

```
extensions=(js jsx md ts tsx)
prettier *.{${extensions[@]}}
```

but that doesn't work: `*.{js: No such file or directory`
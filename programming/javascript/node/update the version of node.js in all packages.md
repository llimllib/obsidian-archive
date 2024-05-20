---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
Just a little bash loop I cooked up that I wanted to save so I remember it:

```bash
for pack in $(fd package.json -E 'bower_components'); do
  tmp=$(mktemp)
  jq '.engines = {node: "18.17.1", npm: "^9"}' "$pack" > "$tmp"
  mv "$tmp" "$pack"
done
```

requires [[fd]] and [[jq]]
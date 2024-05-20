---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://codeberg.org/SimpleWeb/SimplyTranslate-Web/src/branch/master/api.md

```
$ curl -s 'https://simplytranslate.org/api/translate/?engine=google&from=en&to=es&text=Hello' | jq
{
  "definitions": {},
  "translated-text": "Hola",
  "translations": {
    "interjection": {
      "¡Aló!": {
        "frequency": "1/3",
        "words": [
          "Hello!",
          "Hullo!",
          "Halliard!"
        ]
      },
      ...
```

Just wraps google translate though I guess
Salvatore Sanfilippo, aka [antirez](https://github.com/antirez) released a [telegram bot library in C](https://github.com/antirez/botlib) recently. While I'm not at all interested in a telegram bot library, I always like to read Salvatore's code, which is uniformly superb.

The bit of code that caught my eye in this release is in [this file](https://github.com/antirez/botlib/blob/ca2f977deeb3455e69e9a8f6b8ba711798dba6e6/json_wrap.c), which implements a simple selector library on top of the [json library he's using](https://github.com/DaveGamble/cJSON). In about 100 lines of code, it implements a function that parses and executes a tiny [[jq]]-like language:

```c
/* You can select things like this:
 *
 * cJSON *json = cJSON_Parse(myjson_string);
 * cJSON *width = cJSON_Select(json,".features.screens[*].width",4);
 * cJSON *height = cJSON_Select(json,".features.screens[4].*","height");
 * cJSON *price = cJSON_Select(json,".features.screens[4].price_*",
 *                  price_type == EUR ? "eur" : "usd");
```

It's a really nice example of just how simple you can make a parser for a tiny language.

I think it'd be fun to re-implement this in another language to understand it better, and I might give it a go at some point.
---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/ada-url/ada/tree/main

> WHATWG-compliant and fast URL parser written in modern C++

The interesting bit to me is that this repo contains a useful tool: `adaparse`, which is a command line program that accepts a URL and prints a json blob with the URL's components:

```
$ adaparse https://github.com/ada-url/ada?arg=bananas
{
	"buffer":"https://github.com/ada-url/ada?arg=bananas",
	"protocol":"https:",
	"host":"github.com",
	"path":"/ada-url/ada",
	"opaque path":false,
	"query":"?arg=bananas",
	"protocol_end":6,
	"username_end":8,
	"host_start":8,
	"host_end":18,
	"port":null,
	"pathname_start":18,
	"search_start":30,
	"hash_start":null
}
```

I wish it split up the query parameters. It's used as a benchmark program, so I suppose it's less useful than [[trurl]]:

```
$ trurl --json https://github.com/ada-url/ada?arg=bananas
{
  "url": "https://github.com/ada-url/ada?arg=bananas",
  "scheme": "https",
  "host": "github.com",
  "port": "443",
  "path": "/ada-url/ada",
  "query": "arg=bananas",
}
```

Or Carl Johnson's `parse-url` (which I had to modify to build on modern go)

```
$ echo 'https://github.com/ada-url/ada?arg=bananas' | parse-url | jq .
{
  "Scheme": "https",
  "Opaque": "",
  "User": null,
  "Host": "github.com",
  "Path": "/ada-url/ada",
  "RawPath": "",
  "OmitHost": false,
  "ForceQuery": false,
  "RawQuery": "arg=bananas",
  "Fragment": "",
  "RawFragment": ""
}
```
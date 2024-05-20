---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/melbahja/got

> Simple golang package and CLI tool to download large files faster 🏃 than cURL and Wget!

...

> Got takes advantage of the HTTP range requests support in servers [RFC 7233](https://tools.ietf.org/html/rfc7233), if the server supports partial content Got split the file into chunks, then starts downloading and merging the chunks into the destinaton file concurrently.
---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/sferik/t

> A command-line power tool for Twitter.

Dan Nguyen gives [a really cool example](https://twitter.com/dancow/status/1577018291595644928) of using it to find something that was on the tip of his tongue:

```shell
t timeline dancow --csv -n 3200 > dantweets.csv
cat dantweets.csv | xsv sort -s 'Posted at' | xsv select ID,Text | 
  xsv search '^RT' | rg '\bai\b'
```
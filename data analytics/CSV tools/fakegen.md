---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/multiprocessio/fakegen

> This program generates a random schema of M columns and then generates N rows of that schema. So all value types within a column across all rows will be consistent. For example, if a value is an int in one row's column, it will be an int in the same column across all other row's.

> It generates JSON by default but can generate other formats like CSV, TSV, Excel, etc.


```
$ fakegen --rows 2 --cols 5 | jq .
[
  {
    "enecate": 1322845113,
    "irruptions": "et tempore suscipit dignissimos odit ut accusantium dolores cumque est dignissimos ut",
    "phototelescopic": "facere non iusto a pariatur vero qui magnam nostrum quibusdam magnam a omnis ",
    "restrictively": false,
    "upwafted": "2020-10-09T21:03:23.109945329Z"
  },
  {
    "enecate": 1771337749,
    "irruptions": "voluptas quis commodi qui commodi soluta ut debitis ipsam reprehenderit odio quaerat ",
    "phototelescopic": "non suscipit illo omnis explicabo omnis omnis quia eligendi quidem suscipit",
    "restrictively": true,
    "upwafted": "1979-01-09T05:20:25.7650053Z"
  }
]
```

switch formats with the `-f` switch:

```csv
$ fakegen -r 10 -c 2 -f csv
seavy,spangle-baby
2070-08-27T17:07:35Z,-28123.3
2063-10-30T15:06:37Z,-82834.6
2066-04-29T00:10:38Z,-74438.5
2006-08-31T11:45:50Z,-85888.4
1981-11-20T20:49:30Z,-78208.3
2065-07-02T12:31:05Z,13387.5
2003-12-29T22:37:19Z,-62472.3
1981-08-29T14:41:20Z,-55740.1
2062-07-09T08:56:47Z,54202.2
2010-05-30T08:28:33Z,-73394.6
```
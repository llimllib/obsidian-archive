To get file created (added to git) and modified (last updated) times from git:

```
$ git log -1 --pretty="format:%cI %aI" README.md               
2021-11-26T20:13:08-05:00 2021-11-26T20:13:08-05:00
```
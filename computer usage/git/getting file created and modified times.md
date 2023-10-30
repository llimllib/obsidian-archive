To get file created (added to git) and modified (last updated) times from git, use `git log` with two format options:

- `cI` is the created time, in ISO 8601 format
- `aI` is the modified time, in ISO 8601 format

```
$ git log --pretty="format:%cI %aI" README.md
2023-10-30T08:18:52-04:00 2023-10-30T08:18:52-04:00
2022-04-28T21:54:00-04:00 2022-04-28T21:54:00-04:00
2022-04-09T22:09:23-04:00 2022-04-09T22:09:23-04:00
2022-04-08T21:36:48-04:00 2022-04-08T21:36:48-04:00
```

The most recent modification will be the second half of the first line, and the first create time will be the first half of the last line.

If you want just the most recent modified time, you can use:

```
$ git log -1 --pretty="format:%aI" README.md    
2023-10-30T08:18:52-04:00
```

and the first created time:

```
$ git log --pretty="format:%cI" --reverse README.md | head -1
2022-04-08T21:36:48-04:00
```

(Note that limiting is done before sorting, so you cannot use `git log -1 --reverse` - you'll get the most recent date instead of the oldest. Thus you can use `--reverse` and pipe it to `head` instead)

Here's the implementation of this I just wrote in python:

```python
def gitstat(dir: str, path: str) -> GitStat:
    """return the created and modified times for a file from git"""
    # Here's an example of what the output looks like for this:
    #
    # $ git -C . log --pretty="format:%cI %aI" README.md
    # 2023-10-30T08:18:52-04:00 2023-10-30T08:18:52-04:00
    # 2022-04-28T21:54:00-04:00 2022-04-28T21:54:00-04:00
    # 2022-04-09T22:09:23-04:00 2022-04-09T22:09:23-04:00
    # 2022-04-08T21:36:48-04:00 2022-04-08T21:36:48-04:00
    #
    # we need to use the -C argument to tell git to look in the notes
    # repository instead of this repository
    #
    # possibly I should add --follow so that this persists through renames?
    # though maybe I ought to consider a rename a recreation of a file? not
    # clear to me whether it's worth it or not.
    times = (
        subprocess.check_output(
            ["git", "-C", dir, "log", "--pretty=format:%aI %cI", path]
        )
        .decode("utf8")
        .split("\n")
    )

    # The modified time is the second timestamp on the first line
    mtime = rfc3339_to_timestamp(times[0].split(" ")[1])

    # The created time is the first timestamp on the last line
    ctime = rfc3339_to_timestamp(times[-1].split(" ")[0])

    return GitStat(ctime, mtime)
```
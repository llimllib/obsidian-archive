---
created: 2024-10-01T12:19:11.675Z
updated: 2025-06-19T21:20:17.704Z
---
Following a [question on reddit](https://www.reddit.com/r/golang/comments/1ft4udf/performance_write_intensive_sqlite_mattngosqlite3/), I got curious about how well golang sqlite bindings (and translations, and WASM embeddings) compare to using C directly.

I'm competent with C, but no expert, so I used the help of an LLM to translate a [[go-sqlite-bench|golang sqlite benchmark]] to C and tried to make it as equivalent to the golang as possible in terms of the work it was doing.

The [test I copied](https://github.com/cvilsmeier/go-sqlite-bench/blob/b0e7d08b69d685fc20fcbf4ac4de5f57b73c3720/app/app.go#L93) is pretty simple: insert a million users into a database, then query the users table and create user structs for each.

The result is just one test, but it suggests that all sqlite bindings (or translations) have trouble keeping up with sqlite in C. All times here are in milliseconds, and I picked the best of two runs:

| library                                         | insert (ms) | ratio | query (ms) | ratio |
| ----------------------------------------------- | ----------- | ----- | ---------- | ----- |
| C sqlite3                                       | 737         | 1.00  | 84         | 1.00  |
| mattn/sqlite3                                   | 1380        | 1.87  | 1036       | 12.33 |
| [crawshaw.io/sqlite](http://crawshaw.io/sqlite) | 1097        | 1.49  | 542        | 6.45  |
| [modernc.org/sqlite](http://modernc.org/sqlite) | 4148        | 5.63  | 966        | 11.50 |
| eatonphil/gosqlite                              | 1017        | 1.38  | 651        | 7.75  |
| ncruces/go-sqlite3                              | 2178        | 2.96  | 611        | 7.27  |
| zombiezen/go-sqlite                             | 1403        | 1.90  | 211        | 2.51  |
| python 3.12.2                                   | 1992        | 2.70  | 1426       | 16.98 |

![[Pasted image 20241001084907.png]]
![[Pasted image 20241001084951.png]]


The tests were run with go 1.23.1 and clang 16.0.0 on an apple m1 mac with 32gb of ram.

This is a deeply non-serious benchmark - I was browsing the web while I was running it, for starters. Still, the magnitude of the results indicates that sqlite in C is still quite a bit faster than any of the alternatives in go.

Somebody on mastodon asked me how this compares to previous versions of go, so I did a brief test of mattn and crawshaw on go 1.19, and found that they were in the range of 10-15% slower, so real progress on making cgo faster has been made in a pretty short timeframe.

The code is available [here](https://gist.github.com/llimllib/4cb06c5fe7439aa7f3cb67a818fa230d#file-sqlite-c) in a gist.

## update

For kicks, I added a python version to the table above; source is [in the same gist](https://gist.github.com/llimllib/4cb06c5fe7439aa7f3cb67a818fa230d#file-bench-py)

_2025 Jun 19_: noticed that the python ratios were not correct and fixed them; I did not re-run any tests
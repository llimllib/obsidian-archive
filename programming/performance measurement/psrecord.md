---
updated: '2024-02-13T19:13:03Z'
created: '2024-02-13T19:13:03Z'
---
https://github.com/astrofrog/psrecord

A simple tool that automates measuring the memory and CPU usage of a process.

I [wrote a bit about](https://adhoc.team/2019/05/01/memory-measurement/) how to do this using a bash script and `ps` a long time ago, but `psrecord` wraps it up into a useful package.

To measure the performance of `make webpack` on a project I'm working on, I:

- installed it with `pip install psrecord`
- Ran `psrecord "make webpack" --log record.log --plot plot.png --include-children`

And got out both a log file and this useful chart:

![[304520684-dd641a43-406f-434c-b915-1be3650ff08f.png]]
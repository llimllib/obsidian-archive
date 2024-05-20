---
updated: '2024-03-19T18:02:08Z'
created: '2024-03-19T18:02:08Z'
---
https://github.com/brentp/gargs

> **gargs** is like **xargs** but it addresses the following limitations in xargs:

> - it keeps the output serialized (in `xargs` the output one process may be interrupted mid-line by the output from another process) even when using multiple threads
> - easy to specify multiple arguments with number blocks ({0}, {1}, ...) and {} indicates the entire line.
> - easy to use multiple lines to fill command-template.
> - easy to --retry each command if it fails (e.g. due to network or other intermittent error)

see also [[rush]], [[mprocs]]. Seems to have inspired some work in this area, but isn't actively maintained.
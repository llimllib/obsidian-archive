---
updated: '2024-04-11T17:53:25Z'
created: '2024-04-11T17:53:25Z'
---
https://github.com/peak/s5cmd

> `s5cmd` is a very fast S3 and local filesystem execution tool. It comes with support for a multitude of operations including tab completion and wildcard support for files, which can be very handy for your object storage workflow while working with large number of files.

> There are already other utilities to work with S3 and similar object storage services, thus it is natural to wonder what `s5cmd` has to offer that others don't.

> In short, _`s5cmd` offers a very fast speed._ Thanks to [Joshua Robinson](https://github.com/joshuarobinson) for his study and experimentation on `s5cmd;` to quote his medium [post](https://medium.com/@joshua_robinson/s5cmd-for-high-performance-object-storage-7071352cc09d):

> > For uploads, s5cmd is 32x faster than [[s3cmd]] and 12x faster than aws-cli. For downloads, s5cmd can saturate a 40Gbps link (~4.3 GB/s), whereas s3cmd and aws-cli can only reach 85 MB/s and 375 MB/s respectively.
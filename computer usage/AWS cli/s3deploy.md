---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/bep/s3deploy

> A simple tool to deploy static websites to Amazon S3 and CloudFront with Gzip and custom headers support (e.g. "Cache-Control"). It uses ETag hashes to check if a file has changed, which makes it optimal in combination with static site generators like [Hugo](https://github.com/gohugoio/hugo).

...

> If you're looking at `s3deploy` then you've probably already seen the [`aws s3 sync` command](http://docs.aws.amazon.com/cli/latest/reference/s3/sync.html) - this command has a sync-strategy that is not optimised for static sites, it compares the **timestamp** and **size** of your files to decide whether to upload the file.

> Because static-site generators can recreate **every** file (even if identical) the timestamp is updated and thus `aws s3 sync` will needlessly upload every single file. `s3deploy` on the other hand checks the etag hash to check for actual changes, and uses that instead.
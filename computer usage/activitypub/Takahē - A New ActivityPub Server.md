https://aeracode.org/2022/11/14/takahe-new-server/

> I have run all my personal projects on "serverless" hosting for several years now - Google Cloud Run, mostly. Having software only spin up on request and not just sit around is great - not just for efficiency, but because it enforces a shared-nothing architecture on you that makes things easy to maintain.

> ActivityPub, however, is a protocol with a _lot_ of background messaging. Every post has to be delivered to lots of individual (or shared) inboxes, you have to look up Actor information and public keys, and more. Mastodon uses Sidekiq - a classic task scheduler - to do this, but it needs a whole bunch of workers to be running at all times.

> I instead want a design where all I need to deploy is a Docker image, a database, and then set up a scheduled task call a URL every X seconds - these are all primitives that are easily available on any modern serverless platform.
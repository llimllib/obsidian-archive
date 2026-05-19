---
created: 2026-05-19T02:32:31.111Z
updated: 2026-05-19T02:32:31.111Z
---
I added adaptive mode to [[yt-transcribe]], my shell script for transcribing youtube talks: https://github.com/llimllib/yt-transcribe

Adaptive mode looks for scene changes, rather than just generating a thumbnail every N seconds. Here's an example, generating a transcript for [Steve Klabnik's talk](https://bsky.app/profile/steveklabnik.com/post/3mm57bk5cis2t) ["Steel, Rust and Truth"](https://llimllib.github.io/yt-transcribe/klabnik-adaptive/)

That talk motivated the work, as I wanted the script to capture all of the slides - it was hard to follow without that.

The actual change is [here](https://github.com/llimllib/yt-transcribe/commit/2fd503b3c984df6fdb02e9abf26df0a2a740d265)
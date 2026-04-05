---
created: 2026-04-03T20:52:00.737Z
updated: 2026-04-05T15:39:26.798Z
---
To connect [[llm]] to apple foundation models, which run locally but with a small window size (4096 tokens), install [llm-apple](https://github.com/btucker/llm-apple):

`llm install llm-apple`

That plugin, which uses [this library](https://github.com/btucker/apple-foundation-models-py) by the same author to wrap Apple's `FoundationModels`, will let you do something like this to ask the local model how to use ffmpeg to clip a video:

```console
$ llm -m apple "how do I use ffmpeg to trim the first 30 seconds of an mp4 file"
To trim the first 30 seconds of an MP4 file using FFmpeg, you can use its
command-line interface with a specific format for specifying the start and end
times. Here's a step-by-step guide:
```

I submitted [a PR](https://github.com/simonw/llm/pull/1393) to add it to the llm [plugin directory](https://llm.datasette.io/en/stable/plugins/directory.html), but it seems like PRs are getting merged very slowly in that repo.

I got the idea for using this from [[apfel]], then I recreated it, then I found that somebody had done it better than me already; so this is me publishing about that.
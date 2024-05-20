---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/llimllib/ytgif

A tool I wrote for quickly creating gifs from youtube videos.

Uses [[ffmpeg]] and [[yt-dlp]]

example:

```
ytgif -start 74.8 -finish 75.8 -nosubs \
    "https://www.youtube.com/watch?v=KlLMlJ2tDkg&t=50s" wow.gif
```

![[wow.gif]]

lots more [examples here](https://github.com/llimllib/ytgif/blob/main/docs/examples.md)
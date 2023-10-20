	Using [yt-dlp](https://github.com/yt-dlp/yt-dlp) (install with `brew install`)

```console
yt-dlp --download-archive downloaded.txt --extract-audio --audio-format mp3 -o "%(title)s.%(ext)s" 'https://www.youtube.com/watch?v=yuoghR-5-Xs&list=PLSdoVPM5Wnne3Q2AxosemsThywhraJ0su'
 ```

to download a video without audio in the best available format:

```
yt-dlp -f bestvideo https://www.youtube.com/watch?v=-wpHszfnJns
```

from the yt-dlp manual:

`bv, bestvideo: Select the best quality video-only format.  Equivalent to best*[acodec=none]`

see the "format selection" section for more

To download auto-generated subs from youtube, add `--write-auto-subs`

```
yt-dlp -f bv --write-auto-subs https://www.youtube.com/watch?v=d3_DjiLLDfo -o schad.webm
```

That will download the subs as a `vtt` file, which can be burned into the video with something like:

```
ffmpeg -i schad.webm -vf subtitles=schad.en.vtt schad-subs.webm
```

see [[ffmpeg]] for more info
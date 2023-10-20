I wanted to create a gif with some light custom text effects, so here's what I did:

![dumb and dumber](https://cdn.billmill.org/static/gifs/redeem2.gif)

1. Create a starter gif using [[ytgif]]

`./ytgif.bash -v -start 30 -finish 46 -whisper-large 'https://www.youtube.com/watch?v=hZ7Pn8asyw8' redeem2.gif`

This downloads the video I want, clips it to the length I want, and importantly logs every command it runs.

After it's done, I grab the final `ffmpeg` command it runs and copy it. In this case, it was:

```
ffmpeg -y -i /tmp/ytgif_cache/vclip_httpswwwyoutubecomwatchvhZ7Pn8asyw8.webm -filter_complex '[0:v] fps=20, scale=640:-1:flags=lanczos, split [a][b], [a] palettegen [p], [b][p] paletteuse, subtitles=/tmp/ytgif_cache/sub_httpswwwyoutubecomwatchvhZ7Pn8asyw8.srt' redeem2.gif
```

2. Convert the subtitles file to [ass format](https://github.com/libass/libass) (this format name makes me laugh every time)

`ffmpeg -i /tmp/ytgif_cache/sub_httpswwwyoutubecomwatchvhZ7Pn8asyw8.srt sub.ass`

3. Customize the subtitle file

In this case, all I did was bold the last line and turn it red:

```
[Events]
Format: Layer, Start, End, Style, Actor, MarginL, MarginR, MarginV, Effect, Text
Dialogue: 0,0:00:00.25,0:00:04.50,Default,,0,0,0,,just when I think you couldn't possibly be any dumber
Dialogue: 0,0:00:04.50,0:00:10.00,Default,,0,0,0,,you go and do something like this.
Dialogue: 0,0:00:10.00,0:00:12.78,Default,,0,0,0,,{\b1}{\c&HFF&}And totally redeem yourself!{\b0}
```

`{\b1}` is markup for bold, and `{c&HFF&}` is markup for red.

All of the docs I've found for the format are horrific, I got the color info from [here](https://gist.github.com/marnanel/87fee222990df53d23a9999d90a4eae2#file-gistfile1-txt-L986) and the bold markup from somewhere else.

4. re-run the conversion to gif

Take the command we saved in step 1, and re-run it with the new, marked-up subtitle file:

```bash
ffmpeg -y -i /tmp/ytgif_cache/vclip_httpswwwyoutubecomwatchvhZ7Pn8asyw8.webm \
  -filter_complex '[0:v] fps=20, scale=640:-1:flags=lanczos, split [a][b], [a] palettegen [p], [b][p] paletteuse, subtitles=sub.ass' redeem2.gif
```
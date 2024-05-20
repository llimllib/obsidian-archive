---
updated: '2024-05-19T20:48:23Z'
created: '2023-10-20T13:54:09Z'
---
convert a movie to a gif: `ffmpeg -i some.mov some.gif`

convert a movie to a gif, with an fps of 20, a width of 640 and a smaller palette: 

```shell
ffmpeg -i some.mov \
  -filter_complex "[0:v] fps=20,scale=640:-1,split [a][b];[a] palettegen [p];[b][p] paletteuse" \
  some.gif
```

clip from the 2nd second of the movie to the 8th, and convert to a gif:

`ffmpeg -ss 2 -t 6 -i some.mov some.gif`

or alternately

`ffmpeg -ss 2 -to 8 -i some.mov some.gif`

or alternately

`ffmpeg -ss 00:00:02 -to 00:00:08 -i some.mov some.gif`

to clip and avoid reëncoding, use `-c copy` and make sure the output format matches the input:

`ffmpeg -ss 2 -to 8 -c copy -i some.mov some.mov`

to add subtitles to a clip and convert it to a gif, create an SRT file then apply it with:

`ffmpeg -vf subtitles=in.srt -i some.mov out.gif`

The subtitle file `in.srt` in this case looked like:

```

1
00:00:00,000 --> 00:00:6,000
If this all seems a little confusing, don't worry, you can always clear things up by checking the official medicare.gov website

2
00:00:06,000 --> 00:00:10,000
Like here, on the "What Medicare Covers" webpage, which, at the time of this video's recording

3
00:00:010,000 --> 00:00:16,000
starts with the question "Is my plan covered"?
```

- [this page](https://amiaopensource.github.io/ffmprovisr/#filtergraphs) has excellent documentation on advanced ffmpeg features

Create a timelapse from a folder of jpegs:

`ffmpeg -framerate 30 -pattern_type glob -i '*.jpg' -c:v libx264 -r 30 -pix_fmt yuv420p timelapse.mp4`

Stabilize a video (from [news.yc](https://news.ycombinator.com/item?id=40408878), untested):

```
ffmpeg -i "$1" -vf vidstabdetect=shakiness=5:show=1 dummy.avi

ffmpeg -i "$1" -vf yadif, format=yuv420p, vidstabtransform=zoom=2:optzoom=0:crop=black -c:v libx264 -b:a 32k stabilized264.mp4
```

Which also suggests this recipe for building ffmpeg with all the bells and whistles (there are many bells and whistles):

`brew install homebrew-ffmpeg/ffmpeg/ffmpeg $(brew options homebrew-ffmpeg/ffmpeg/ffmpeg --compact)`
---
created: 2024-08-21T12:34:20.610Z
updated: 2024-08-21T12:34:20.610Z
---
https://tratt.net/laurie/blog/2024/recording_and_processing_spoken_word.html

Larry Tratt's advice on how to get decent quality out of your office's sound.

- Use a USB mic
- dampen the sound in the room
- record without clipping
- compress the dynamic range with `ffmpeg`:
```
ffmpeg -i in.flac \  
  -af "acompressor=threshold=-24dB:attack=2.5:release=15:ratio=3" \
  out.flac
```
- normalize with `ffmpeg-normalize`:
```
ffmpeg-normalize <input file> -o normalised.mp3 \
  -c:a mp3 -b:a 96 -pr -t -16 -tp -1
```
---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/jdek/openwith

A utility for specifying what application should open what file type from the command line

```
$ osascript -e 'id of app "mpv"'
io.mpv
$ openwith io.mpv mkv mov mp4 avi
```

^^^ first we get the application id of `mpv`, then set it to open `mkv`, `mov`, `mp4`, and `avi` files

Not available on homebrew.

Example of me setting firefox as my program for opening gifs, because preview handles them in an insanely useless way:

```
$ openwith $(osascript -e 'id of app "firefox.app"') gif
gif (com.compuserve.gif) -> org.mozilla.firefox
gif (com.apple.private.auto-loop-gif) -> org.mozilla.firefox
```

It kind of annoyingly opens them in a new window instead of a tab, but what can you do
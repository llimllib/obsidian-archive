Using the fontconfig backend like so:

`pango-view -t "κόσμε🔥🇯🇲" -o /tmp/test.png --font "Ubuntu 50" --backend=ft2`

You can come close to getting proper emoji fallback, but you get a mono emoji and very poor spacing:

![[test 2.png]]

with the cairo backend, it doesn't get that close, showing no emoji at all:

`pango-view -tκόσμε🔥🇯🇲" -o /tmp/test.png --font "Ubuntu Mono 50" --backend=cairo`

![[test 4.png]]

I wonder if this is a homebrew failure? I should retry with a linux distro.
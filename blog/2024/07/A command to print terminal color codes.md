---
created: 2024-07-19T13:05:13.988Z
updated: 2024-07-19T13:05:13.988Z
---
I write shell scripts that use terminal colors often enough that it's handy to know a bit about them, but not often enough that I remember how they work without looking it up.

So, this morning, I wrote `colors`, a shell script that prints out tables of the basic ANSI colors and text effects, and demonstrates what they look like on your terminal.

[Here's the script](https://github.com/llimllib/personal_code/blob/master/homedir/.local/bin/colors), and here's what it looks like on a mostly-stock apple terminal.app with a dark color scheme:

![[Pasted image 20240719093855.png]]

You can pass `-v` to the script to get a table of the 8-bit colors, in case you want to get real fancy with your script:

![[Pasted image 20240719094123.png]]
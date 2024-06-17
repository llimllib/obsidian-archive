---
created: 2024-06-17T13:20:18.769Z
updated: 2024-06-17T13:20:18.769Z
---
The always excellent Julia Evans [notes](https://social.jvns.ca/@b0rk/112632058299461831) a better command to list all listening ports and the process listening to them on a mac. `sudo lsof -i -P` is often given as a command to use, but it is very slow and hangs for a long time.

She suggests `sudo lsof -iTCP -sTCP:LISTEN -iUDP -n -P` instead.

I've hit this problem before; when debugging [this issue](https://stackoverflow.com/questions/51071020/golang-net-listen-binds-to-port-thats-already-in-use), somebody suggested `lsof -I -T f | grep 8888` and it was super slow; eventually I found that `lsof -i :8888 -T f` was much faster.

I don't truly understand what lsof is doing though.
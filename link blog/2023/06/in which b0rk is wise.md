https://social.jvns.ca/@b0rk/110628907743101469
https://social.jvns.ca/@b0rk/110628916255208525

> i'm working on a thing with a terminal in a browser and I can't believe I wasted so much time in the past trying to find a Go library that could act as a backend for [xtermjs.org/](https://xtermjs.org/) when it seems so much easier just to write it myself from scratch? like I think it's literally just a few lines of Go gluing together [github.com/creack/pty](https://github.com/creack/pty) and [github.com/gorilla/websocket](https://github.com/gorilla/websocket), plus some code to resize the pty when the browser's screen resizes

> very grateful to my past self for writing [jvns.ca/blog/2022/07/28/toy-re](https://jvns.ca/blog/2022/07/28/toy-remote-login-server/) which I needed to read to remind myself how terminals work
---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://github.com/simsong/tcpflow

Found via https://ananthakumaran.in/2022/11/12/trace-http-requests.html which describes it thus:

> `tcpflow` can analyze the data transmitted via tcp sockets. It can look at any live tcp socket and show the back and forth communications. You might think, this sounds very similar to `tcpdump`, it is, with one twist, it understands the HTTP protocol and shows the HTTP request and response in a meaningful way. The flag -c sends all the output to stdout, without that, multiple files will be created representing the request, response, and decoded body. It can decode gzip encoded response as well.
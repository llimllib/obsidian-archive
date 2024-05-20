---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
> When thinking about streaming data on the web, most people’s thoughts will immediately turn to WebSockets. It turns out, if you don’t need bidirectional communication, there is a much simpler and well suited technology that accomplishes this over normal HTTP connections: [Server-Sent Events (SSE)](http://www.html5rocks.com/en/tutorials/eventsource/basics/).

> I won’t go into detail about the SSE protocol (the above link is a great resource for learning more about it), instead I’ll just say it’s trivially easy to handle SSE in Javascript, for example the full logic for subscribing to an event source and passing events to a callback handler can be accomplished in a barely more than a single line of code. The protocol will automatically handle reconnections, etc. The more interesting aspect for us is how we handle this on the server side.

- https://medium.com/@mroth/how-i-built-emojitracker-179cfd8238ac

I had never heard of these! That's a useful trick.

I got there from [this demo](https://github.com/dacort/golang-sse-demo) of how to use them in [[golang]]
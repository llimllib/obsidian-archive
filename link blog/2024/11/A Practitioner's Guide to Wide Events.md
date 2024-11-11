---
created: 2024-11-11T13:39:31.884Z
updated: 2024-11-11T13:39:31.884Z
---
https://jeremymorrell.dev/blog/a-practitioners-guide-to-wide-events/

I like this walkthrough of the many things you can add to your wide events.

I've had great success with wide events since I implemented them on [[Serving a billion web requests with boring code]], and my method has always been to inspect the request and response objects and add anything to the event that could possibly be releant. It's helpful to have a list to browse and think of what you might be missing.
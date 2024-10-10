---
created: 2024-10-09T14:21:02.094Z
updated: 2024-10-09T14:21:02.094Z
---
> An exercise that I try to do every once in a while is to “step a frame” in the game, starting at some major point like common->Frame(), game->Frame(), or renderer->EndFrame(), and step into every function to try and walk the complete code coverage. This usually gets rather depressing long before you get to the end of the frame. Awareness of all the code that is actually executing is important, and it is too easy to have very large blocks of code that you just always skip over while debugging, even though they have performance and stability implications...

> If something is going to be done once per frame, there is some value to having it happen in the outermost part of the frame loop, rather than buried deep inside some chain of functions that may wind up getting skipped for some reason.

- [John Carmack](http://number-none.com/blow/blog/programming/2014/09/26/carmack-on-inlined-code.html)
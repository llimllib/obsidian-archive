https://blog.plover.com/prog/vertical-complexity.html

>  Wrapping up code this way reduces _horizontal_ complexity in that it makes the top level program shorter and quicker. But it increases _vertical_ complexity because there are now more layers of function calling, more layers of interface to understand, and more hidden magic behavior. When something breaks, your worries aren't limited to understanding what is wrong with your code. You also have to wonder about what the library call is doing. Is the library correct? Are you calling it correctly? The difficulty of localizing the bug is larger, and when there is a problem it may be in some module that you can't see, and that you may not know exists.

...

> adding code and interfaces and libraries to software has an obvious benefit: look how much smaller the top-level code has become! But the cost, that the software is 0.0002% more complex, is harder to see. So you keep moving in the same direction, constantly improving the software architecture, until one day you wake up and realize that it is unmaintainable. You are baffled. What could have gone wrong?

...

> My co-worker... wrote:

> > The better we can hide how the sausage is made the more approachable and easier it is for those who build on it to be productive.

> In some educational contexts, I think this is a good idea. But not if you are trying to teach people sausage-making!
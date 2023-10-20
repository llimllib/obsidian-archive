https://thelig.ht/ui-apps-are-broken/

> Once I realized that I had to additionally take real-time constraints into account while building, it drove a lot of the engineering decisions I made in a specific direction. In particular, the worst case time of every sequence of code must be accounted for, the average-case time was irrelevant for correctness...

> Armed with this new awareness, I began to notice the lack of real-time discipline in other applications, including my own. This was a jarring experience, how could I have never noticed this before? The juggernaut during this period was when I realized that most mainstream desktop UI applications were fundamentally broken.

> When I click a mouse button, when I press a key on the keyboard, I expect a response in a bounded amount of time. Bounded amount of time? We’ve heard this before! UI applications are also real-time systems. How much time is this bounded amount of time? 100ms or maybe 250ms. Well, take your pick, the key point is that the response time should not be indefinite. I should never see a beach ball of death. Never.

I think a lot of the early success of node was built on something like this: async by default meant that UI event handlers (and web handlers etc) were not waiting on file reads/network reads/etc and this encouraged a more responsive style of programming. Not quite real-time, but it had a similar effect.

> As far as I can tell, fixing this in a meaningful way will require large ecosystem-level changes and broad awareness. Lots of wide-reaching architectural decisions that ignore these issues have accumulated over decades. I’m tempted to abandon using Windows, macOS and Linux as the main platforms with which I interact.

This seems like throwing the baby out with the bathwater - surely we could focus on patterns to encourage responsive programs but also keep our time-sharing virtual memory systems.
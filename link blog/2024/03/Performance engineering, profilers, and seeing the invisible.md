---
updated: '2024-03-25T18:08:44Z'
created: '2024-03-25T18:08:08Z'
---
https://blog.nelhage.com/post/profilers-seeing-the-invisible/

> Klein and Hoffman [discuss the ability](https://cmapspublic3.ihmc.us/rid=1G9NSY15K-N7MJMZ-LC5/SeeingTheInvisible.pdf) of experts to “see what is not there”: in addition to observing data and cues that are present in the environment, experts perceive **implications** of these cues, such as the absence of expected or “typical” information, the typicality or atypicality of observed data, and likely/possible past and future time trajectories of a system based on a point-in-time snapshot or limited duration of observation.

> I want to talk about some of the ideas of that piece in the specific context of performance engineering, and what profilers can and cannot do for you. In particular, I think this piece makes a great lens for discussing why profilers are both invaluable tools and yet also not the be-all and end-all of performance engineering...

> Experts, especially domain experts in a particular application or programming language or framework, can often look at a profiler and “see” the answers to many of the above questions, even thought they are not literally present in the profile.

> They can “read between the lines” to ask and even answer the “right“ or “better” questions, instead of stopping at the questions literally answered by the profiler. Additionally, and importantly, when they can’t do so for one reason or another, experts will be much faster to **recognize** that that the profiler is asking the wrong questions, and find or build another tool, instead of continuing to bash their head against the same profile in the hopes that it will somehow yield an understanding it does not contain.

Nice article about how you can't just blindly follow a profiler's information to optimize a program.

I haven't read the linked paper yet but I'd like to.
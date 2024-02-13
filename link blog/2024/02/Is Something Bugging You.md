https://antithesis.com/blog/is_something_bugging_you/

> And here we were, trying to make a software system that would behave _perfectly_ and maintain its ACID guarantees in the face of all of this. How were we going to do that?

> So we did something crazy, which turned out to be the best decision we made in the whole history of the company. Before we even started writing the database, we first wrote a fully-deterministic event-based network simulation that our database could plug into. This system let us simulate an entire cluster of interacting database processes, all within a single-threaded, single-process application, and all driven by the same random number generator. We could run this virtual cluster, inject network faults, kill machines, simulate whatever crazy behavior we wanted, and see how it reacted.

----

> Here is the cool part of the story. The cool part is what happened after we found all the bugs in the database. You see, once you’ve found all the bugs in something, and you have very powerful tests which can find any new ones, programming feels completely different. I’ve only gotten to do this a few times in my career, and it’s hard to convey the feeling in words, but I have to try. It’s like being half of a cyborg, or having a jetpack, or something. You write code, and then you ask the computer if the code is correct, and if not then you try again. Can you imagine having a genie, or an oracle, which just _tells you_ whether you did something wrong?

---

One of the authors of [[FoundationDB]] talks about why their extremely thorough testing strategy was a superpower, and about their new startup that tries to bring this sort of testing to other software.
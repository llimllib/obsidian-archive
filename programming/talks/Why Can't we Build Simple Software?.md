---
updated: '2023-10-20T13:54:09Z'
created: '2023-10-20T13:54:09Z'
---
https://vimeo.com/780013486 by Peter van Hardenberg

via this toot https://hachyderm.io/@allafarce/109605444838150996

Transcript via [[whisper]]

```
You are many things, and I can't explain it properly.
So you should introduce yourself.
But yeah, your microphone's right here.
Yeah, press hard for the next slide, backwards,
and a pointer if you need it.
Great, thanks.
Thank you so much.
Hi, everyone.
I'm Peter.
I'm going to kind of take things in a bit more
of a philosophical kind of direction.
You know, I work for a research lab these days,
so that's kind of my tendency.
The lab is called Ink and Switch.
We are interested in carrying on kind
of the work of Engelbart and Licklider and Alan
Kay and these people.
We're interested in how computers
can augment human intelligence.
And that's very highfalutin.
It's a lot of fun.
We get to dig into all kinds of weird corners of software
and experimental interfaces and so on.
But before that, I have written a lot of production software.
So I'm not just speaking to you from kind of an ivory tower
perspective.
I was one of the early employees at a platform
as a service company called Heroku.
I've run a lot of Postgres databases.
I've worked in game development as well.
I've built titles for DS and GBA.
I worked on this one, Teenage Zombies,
Invasion of the Alien Brain Thingies,
for a Victoria, BC game company.
And I've worked on desktop software
like Songbird, which was a cross-platform media player that
lost fairly decisively.
And besides that, I've also worked in research,
spending some time on, for example, this ship here,
the Sir Wilfrid Laurier.
It's a Canadian Arctic research icebreaker.
So I spent some time in the Arctic.
And that actually helped inform my perspective on things too.
But we'll come back to that.
So I want to start by kind of saying, well, hold on a sec.
Before we get into kind of talking about why we can't make
simple software, we should probably
define our terms a little bit and talk about what
complexity actually is.
So the first thing I want to clarify is that complexity
is not difficulty.
Just because something is hard doesn't mean it's complicated.
The ideas of calculus might be very difficult to internalize,
but they're actually very simple and elegant.
And I also want to draw a distinction between something
being complex or just being kind of big.
A box of Lego is not necessarily a complicated thing,
though you can make a lot of things with it.
Complexity occurs when your systems
interact with each other and when
it takes a lot to get things done because of that.
And more specifically, I think the problem with complexity
is that your systems can become unreasonable.
And when I say unreasonable, I don't
mean in kind of like a sort of colloquial sense.
What I mean is that you literally
cannot reason about them.
You don't have the ability to predict
what's going to happen.
And a lot of the time, that's a problem
because you've got work to do and the thing is crashing
and you don't know why.
But a complex system can also be generative and surprising
if you harness that complexity in positive ways.
Last, before we get into it, I want
to make just a very small detail point for the more
pedantic in the audience.
Some people draw a very specific difference
between complex systems from sort of chaos math and emergent
complexity.
We'll talk a little bit about that.
As distinguished from complicated systems
where you have a lot of just kind of mess,
I'm kind of going to float back and forth
across both of these without a lot of distinction
because I think in this context, either one
can cause similar effects.
OK.
So we're going to begin with a non-comprehensive look
at complexity.
And more specifically, we're going to kind of cherry
pick some examples from fake industrial scenarios
where you can begin with something simple
and end up with something complicated.
So I'm going to start with the most basic of all reasons
why your software gets complicated.
And that's the first version of your code.
You just write the happy path.
Everything's glorious.
And software can be really simple
when it lives in an idealized world and everything is fine.
And so here's like a really simple imaginary pseudocode
web thing.
Great.
We've got a GET request to our application.
We're going to go fetch something from the database
and say, hello there.
This is a Hello World app of web apps, server apps.
Great.
And it works fine if user 12 is me,
and user 10 is my friend Keiko, and user foo is wait, what?
Right.
We've got to validate the input.
OK, so we'll validate the request.
Now, OK, so we're validating the request, and that's good.
And oh, jeez, I'm not really handling it
if we don't validate the request.
And wait, do I have to do this on every request?
I guess I have to do this on every request.
And am I doing it the same way on every request?
In fact, this exact pattern of validating user input
and checking your arguments can lead to something
that Bradis and Patterson call shotgun parsing.
And shotgun parsing is kind of the idea
that you're parsing your input, but it's
like someone's taken a shotgun to your code base
because it's just blown through the whole code base.
And it can lead to very serious security vulnerabilities
because you might carefully check an input in one place,
but not in another.
And there's a great talk from Brucon 2012 about this.
So of course, now we're going to be a little more careful.
So we're going to also, if the database is down,
we don't want to send a 500.
We're going to fail elegantly.
And as you go, the more of these cases that you have to handle
and the better the quality of your code
is, the more conservative, defensive, thorough
that you are.
At this point now, the actual logic of this method
is beginning to disappear into all the edge case handling.
We're well off the happy path now.
And so you can clean this up a little bit.
So imagine here in this case that we
have a slightly better set of libraries,
more thoroughly written set of libraries.
We've moved the complexity down out of this method.
And we're sort of saying, well, the database
won't throw an exception, because exceptions are
ugly and kind of subtle to handle.
Well, it'll return null if it can't
do the job for whatever reason.
And we're going to say, well, there's
like a good type system that's handling parsing the input
args before they get to us, so we don't have
to worry about that anymore.
And the value of well-written libraries and languages,
type systems, and so on is that they can really
simplify your code, make it less complex by preventing you
from having to carry around all of this mental state
everywhere that you go.
And my observation of this world is
that vigilance is not a strategy.
We talked earlier about how if a system fails,
it's not, oh, blameless postmortems.
It's not that the developer failed.
It's that the system failed.
If you have security vulnerabilities in your code
because you didn't handle input, the answer
isn't to berate yourself for not handling the input.
It's to step back to level up and say, well, hold on.
Why do I have to do this manually every time?
So strategically, you want to minimize the scope of failures
and kind of design them out of your system.
And one way to do that is to have a type system
so you don't forget to check your nulls.
There are other approaches.
I don't think this is universally true,
but it's one way.
OK, so let's talk about scale.
We all know as an array gets bigger,
you can have an O of n log n kind of sort algorithm.
Great, OK, well, scale's easy, right?
So let's just imagine an admin panel for a web application.
You list your users.
It looks kind of like this.
Go to your database, select all the users,
and then in your front end, just show them all.
Perfect, easy, it's fine.
You've only got 10 users, who cares?
OK, well, now we're at 10 to the 4.
OK, you've got 1,000 users or so.
OK, well, OK, we can't just render all that on one screen.
OK, well, we're going to use one of those offset SQL things,
right?
We know about this.
And then we're going to need pagination, I guess.
And you've got to click through.
OK, yeah, sure, we can still do this.
This is fine.
You don't want to request all that.
It's a pain to scroll through.
OK, well, now we're 10 to the 6 users.
We've got a million.
Actually, that offset thing, that's
a problem if you have a lot of users,
because in order to generate page 850,
it actually selects all of those rows and scrolls through them
and just takes all of those results
and just chucks them on the floor
until it gets to the ones that you asked about.
And actually, now, even though nothing
has changed about our problem statement,
not only are the performance characteristics of the system
starting to change and the user interface is starting to change,
but the way that we interact with the problem
is changing, too.
Because if you've got a million users,
the way to find a user is not to just keep clicking Next
until you find them one page after another.
Oh, page 350, OK, I'm on the Js.
OK, click forward to change the query arg to force it.
We've all done these kinds of things
when the tools didn't keep up with our admin systems.
But the point I'm trying to make here
is that once you start to reach 100 million users,
it's not even the same kind of problem anymore.
The complexity that snuck in here
is now that we have different responsibilities.
There are ethical, there are legal,
there are policy responsibilities.
You probably have a team of people
at your organization who are responsible for dealing
with abuse.
Some of these people are terrible,
and you want them off your platform,
and you can't find them, right?
Like, it's a different thing.
And it's complicated because the environment has changed
as much as anything else.
So everything changes when your scale changes.
It's not just like an algorithmic thing.
It's also the kinds of things that you're doing change.
And in general, my advice to someone
who's built a lot of high-scale production systems
through many orders of magnitude is
that it's as harmful to build for the system of the future
as it is to build an insufficient system
for the present.
If you build the tools for 100 million users
when you have 100 users, they're going
to be completely unusable, too.
And you're going to waste so much time trying to solve
problems you don't have yet that you're
going to miss out on all the benefits of being
able to just look at all your users
and see who they are and talk to them, right?
So you need to be scale-appropriate and kind
of be looking ahead.
Another way software can get complicated
is with leaky abstractions.
And so here we have a platform that's a little bit skewed.
And so complexity can kind of bubble up
from under the waterline through these imperfect abstractions.
This is how you copy a string.
It's a nice handmade, low-level.
This is an excerpt from Kernighan and Ritchie, 1988,
second edition, C programming language.
And this book was such a revelation for me,
like how it showed me the way kernel functions were really
implemented.
No, I'm just kidding.
They're not really implemented like this.
They say here that this is how a C programmer would
prefer to write string copy.
The C programmer in question has never
forgotten to null terminate a string, I see.
But this is how string copy is actually implemented as of 2022
for alpha in Linux.
And actually, this isn't how string copy is implemented.
This is like one page of assembler.
There's like 300 lines of assembly.
And really importantly and intriguingly,
although the interface remains the same,
modern CPU architectures have so many more constraints
around memory alignment and everything else
that although the interface is preserved,
you can pass any pointers in and get values back,
the kind of performance characteristics
of doing an unaligned versus an aligned string copy
will be dramatically different.
And so complexity here, I think we can kind of call this a win.
We've got this super powered computer under the hood now,
but it still kind of feels like that old jalopy
they were running in 1988.
And that's cool that it works.
But in a sense, this API that's so simple
is actually undermining the value of the system.
And there's a lot of magic happening to kind of hide this.
And so I feel very mixed about this,
because on the one hand, it's sort of like SQL databases
where you can add an index and change nothing else
and things get faster.
But there's a really important, subtle lie
that's being told here.
But maybe this is good and maybe it's bad.
This is like a value judgment kind of question.
And whether you understand this is happening
could be completely irrelevant, or it
could be the difference between the success
and failure of a project.
OK, so these are kind of like technical complexities
that come in.
I want to talk about other sources of complexity,
different kinds of complexity.
And one really big source of complexity in my projects,
maybe you're smarter than me and that's cool,
but it's when you have a gap between the problem you think
you have or the problem you used to have
and the problem you have right now.
And again, we're going to use a toy example to illustrate this.
So you've got a users table, just the same app as before.
And your users is a bunch of fields.
You've got a first name and a last name.
And how do you get the first name and the last name?
It's easy.
Guys, you just split on a space.
As a Van Hardenberg, you can see how
this might get you in trouble.
And in fact, on my California driver's license,
it said that my middle name was Van for many years.
And the problem here is that the model
that you have for the problem doesn't actually
map the problem domain successfully.
So what do you do?
And there are lots of things you can do.
You can rewrite from scratch.
You can patch around it.
And actually, just as an aside for everybody in the room,
the W3C has a wonderful essay about personal names
around the world.
And if you take one little thing from this talk,
don't use first name and last name.
Don't use family name.
People's family names aren't accurate.
Some people have them, and others don't.
What you do is you have one field that
is, what is the full name?
And then the other one is, if you need it,
what should we call you?
It's a much better model.
Also, Unicode.
I know that's its own set of complexity, but.
And so there's only so many things
you can do when you have this problem.
And I had a really specific, concrete example
of this in a distributed system recently,
where I had a mental model of how the system behaved.
And my tests demonstrated that it behaved that way.
And then in my production environment,
it behaved completely differently
because of behaviors that were not
modeled by my understanding of the problem.
And this is part of why distributed systems are
so prone to this, is because there's
so many new free variables and articulation points where
things can be fast or slow, or where they can fail or arrive
out of order, and all these kinds of things.
And so when you have these kinds of model reality gaps,
you have to bridge them somehow.
And so what can you do?
Well, you can fix the problem.
You can improve your understanding
and rewrite everything.
And when you can do that, it's probably best.
You can't really always do that, though.
And more to the point, you could see the problem,
but you may still not actually understand the solution.
And so what can you do?
Well, you can hack around it.
I've put Van Hardenburg into a lot of text boxes
without a space in it, where the first letter is capitalized
and the H is lowercase.
And that's not how I spell my name,
but it is how a lot of systems spell my name.
Or you can ignore the problem.
Maybe it's fine.
And genuinely, it could be fine for your use case.
You're just like, well, I guess that Peter guy can suck it.
He'll deal with having his name spelled wrong.
And I do.
These are options that you have.
And there's a great meme series out there on the internet,
lies programmers believe about pretty much anything.
All time zones are one hour apart, half an hour
later in Newfoundland.
And so I think this is a very fundamental source
of complexity.
But where things get really bad is
when your problems start to multiply off each other.
And this, of course, is where you
have compound interest on complexity.
So what happens if your problems dimensionalize
against each other?
So again, imagine this web application.
You've got a bunch of different browsers to support.
You've got a bunch of different runtime environments
to support, different screen sizes, network speeds,
different OS or browser versions.
And so if you want to actually understand what's happening,
all of these things multiply against each other.
And so you don't just have one runtime environment.
You might have one code base.
But you have lots of different contexts.
So how can you know that you actually
have correct functioning code?
Because the old joke about Docker,
like, well, it worked on my computer.
Well, I guess we'll ship your computer.
Well, even that doesn't really work.
Because once you get out into the real world,
there's different memory contexts,
or you're up against different loads, or whatever else.
You don't actually control the whole environment.
And so this is what really starts
to kill you with complexity.
And it's where all of those smaller inconsistencies
play off each other to create an unknowably complicated
environment.
And this is why you see so much popularity.
And Ember Jen were kind of hinting at this,
like, you don't use the native APIs, because God help you
if you're trying to figure out how
to map all of these totally different environments
down to one consistent thing.
And one solution here is just to only have one thing as best
you can and to minimize the difference
between those environments.
And that's why you see ostensibly lazy Electron
apps from big companies.
Because even worse than having to support
all these different things is having
to coordinate all the different people and teams
to try and build features.
And many of us have been there, right?
Like, if you have an iOS and an Android team,
like, how do you get them to ship the same feature
in the same quarter?
It's tough.
It's tough.
OK, so I hope I've convinced you now
that complexity is a complex problem itself
and that it manifests in a lot of different ways.
So we're going to change gears a little bit
and talk about seatbelts.
And more specifically, why seatbelts don't save lives.
And I have an asterisk here, because this
is a little bit of a controversial research topic.
But the sort of upshot of this is
that in at least some studies, they
found that after seatbelts became mandatory in cars,
people still died on the roads at similar rates.
And that was really surprising, because seatbelts
are a good idea.
Like, they keep you safer in the car.
And so somebody proposed this idea called risk homeostasis.
The idea behind risk homeostasis is
that actually we die at a rate on the road related
to how much risk we're willing to take.
And so if you now have a seatbelt
and you're driving a car that's safer,
you're going to go a little faster
and you're going to take the corners a little tighter,
because you feel better.
So the issue with making people safer
was that they then took on more risky behavior,
conserving their total risk tolerance.
And so I think we see a similar thing in software.
I call this complexity homeostasis,
which is to say that if you have kind of a system that's
evolving over time, everything's fine, we're going along,
life is good, and then we add some more things,
and we're still happy.
And then, oh, yeah, now I don't like it anymore.
That's not good.
It feels bad now.
It's time for that rewrite that we were hearing about.
It's time to bring things back.
OK, now we can go back to making things complicated again.
And so this is kind of like a set point.
So homeostasis is the process where our,
or it's any process where you sort of maintain a set point.
And it's commonly used to talk also about how our bodies
regulate temperature.
But I think our organizations regulate complexity.
And so all of us have different intuitions.
And when people talk about wanting things to be simple,
there's like an aesthetic preference here.
And different people perceive that and pursue
that differently.
And like Devine's quest for just the right number of opcodes
that we heard about yesterday is a great example,
where in a certain sense, the correct number of opcodes
is one, and you could do that if you really wanted to.
But then you've got kind of like the CISC model,
where actually the correct number is hundreds,
because you're maintaining backwards compatibility.
And anything that can squeeze you either better numbers out
of a benchmark or more CPU sales is acceptable.
And so how you perceive what constitutes complexity
or how much complexity you're willing to tolerate
is an individual or an organizational decision.
And some things can actually move that up.
Like I have abandoned projects because they
got complicated and annoying to work on.
But some people might just tolerate that and not
perceive it.
I've worked with some brilliant people
who write the most complicated, insane, convoluted code
from my perspective.
But when I sort of go to them, I'm like,
this is so complicated and weird.
Why did you do it this way?
They don't see it, because they're just much smarter
than me.
They're able to hold that complexity in their head
comfortably.
And so for them, it doesn't feel that way.
Another way a system can become more complicated,
if it's worth a lot of money.
Because you can just hire another poor schmo
to sling Java into the code base.
I mean, has anybody here worked on an EA Sports title?
Yeah, I'm so sorry.
I have heard some things, man.
And it ships every year on deadline without fail, right?
That's not an environment that leads to healthy refactoring
or reduction of complexity.
But you know what?
It makes a boatload of money.
And so they'll hire people to work on it,
because they can afford to.
And you'll work on it, because they'll pay you enough.
Because they know.
They know.
And so part of this, as well, is that also,
if you just have more people working on things,
you can tolerate more complexity.
I can hold part of it in my head,
and you can hold part of it in your head.
And I kind of want to distinguish,
there's sort of the breadth of complexity.
And if you have a well-factored system,
you can decompose the complexity,
either into layers or modules.
Like each individual LEGO brick is simple,
but you can build very complicated things from it.
And so that's sort of the system complexity
versus the component complexity.
CSS is incredibly complicated.
And by that, what I mean, it's complex.
You can't tell from looking at one rule what it will manifest
as in a final document.
So OK, well, we can just solve this problem with better tools,
right?
Well, no.
Because as we've talked about, we
have this homeostasis point that we fall towards over time.
And we can choose where to set it,
but we do move towards it.
And the research on this actually
goes all the way back to the 1860s.
This is Jevin's paradox, which was like,
why did coal consumption not decrease when engines
became more efficient?
And the answer is, people did more work, right?
And so I feel very much that this
is sort of the inevitable conclusion
we have to draw from looking at the problem, which
is that the degree of complexity of a system
is tied to who we are and what we're doing over time, right?
And so when we buy back some complexity
by using better tools or by picking a simpler environment,
we're going to spend that out again eventually.
OK, so let's talk a little bit about some theories
of complexity, because I'm from a research lab,
and I like to read papers.
So this is not a new problem.
Have people heard of cyclometric complexity before?
Yeah, we're not going to do this.
You're welcome.
But I do think that although the naive pursuit of software
metrics as a way of measuring what we're doing is not wise,
I think that the conceptual understanding
that when you couple things together that can have a cost
and be problematic is worth thinking about.
In fact, people have been looking at this
and thinking about it since the 1980s.
This is Merrill Lyman in 1980s IEEE volume 68.
So this is not a new domain.
And so even back then, this edition was from 1980.
The first paper published was in 1974
on these laws of software engineering.
We're not going to read these super close.
It's more that I want you to realize
that this kind of recognition that systems
grow to meet growing needs if they're successful
is not a new idea.
It's a common problem.
And whether you're working in building tools or languages,
you might start with an elegant and simple thing.
But as a system has more demands on it, it responds by adding.
That's a very common, and it's a reasonable consequence.
And if you don't do those things,
the thing will often starve and die.
One great paper, if you haven't read it yet, on this topic
is Out of the Tar Pit by Mosley.
This is from 2006.
And this paper differentiates between
what is accidentally complex versus essentially complex.
So essential complexity is the irreducible, non-eliminable
part of your system.
If you are trying to model certain physical processes
like smoke or fire, the physics part where you're actually
doing the work, you can't get rid of that.
You don't want to get rid of that.
That's what you're here for, right?
But the accidental complexity is all that other stuff,
like, oh, god, we've got to compile this so it works on.
Windows 11 has changed the ABI for this DLL.
All that stuff where we heard about Devine hoisting
the phone up the mast to download 11 gigs of something.
That's mostly accidental complexity for our purposes.
And so it helps as you're working and thinking
about complexity to think about where you're spending
that budget and whether you're being deliberate in terms
of how you're adopting complexity.
The other thing I want to refer to
is this great essay from the Berkeley DB
team in The Architecture of Open Source.
And honestly, I highly recommend reading this
if you just like software engineering.
The Architecture of Open Source Software is a cool series.
And basically, what they do is interview open source
communities about their software and have
them write essays about what they've done,
and then they publish and share those.
But I think this Berkeley DB chapter in particular
is exceptional.
And I think about this all the time,
which is that software architecture degrades
with changes made to software.
So you might have the most elegant, brilliant, carefully
planned system in the world, but it does not
exist at a single point in time in a vacuum.
And as new demands come along, this architecture will decay.
And so it requires a constant shoring up.
And when you have big interfaces that you've invested heavily
in and they're straining, it can be extremely expensive
to change them.
I also just love this, because it's
a little more handmade, specific kind of vibe.
The Excel team motto, at least according to Joel Spolsky,
is find your dependencies and eliminate them.
I have been told on reasonably good authority
that Excel actually is built with its own C compiler,
that they didn't even want to rely
on other teams within Microsoft, and to the degree
where they've built their own compilers.
I'm not saying you necessarily should do that.
I'm not saying you necessarily shouldn't.
You've got to think about how you're spending your budget.
And the last kind of point I want to make on this theme
is, again, that complexity isn't necessarily bad.
Complexity can lead to all kinds of wonderful emergent
properties.
The Legend of Zelda, Breath of the Wild,
it has had such a wonderful community grow up around it
precisely because they managed to tame complexity
with their chemistry engine.
So there's a lot of emergent gameplay properties
and experiences that come out of interactions,
complex interactions between systems,
but the systems are factored in a way that
enables and empowers this.
And of course, if you're a roguelike fan,
people have been doing this forever there.
OK, so now what?
We have now looked at complexity.
I've told you you can't get rid of it.
So we're just going to have to live with it.
And better tools won't save us.
So how are we going to spend this complexity budget
that we have?
I mean, one approach is you just put your head down
and you work away and pretend it's not a problem.
And that's a pretty common solution
to all of our problems in life, so we could do that.
But I'm going to maybe try and propose a few ways
we can cut the Gordian Knot here.
And so the story of the Gordian Knot
was that there was this ox cart with a really complicated knot
on the handle.
And people were like, oh, whoever unties this knot
will rule all of Asia.
And many people had come.
And then Alexander the Great came along.
And depending on the version of the story you hear,
he's like, OK, cool.
And he cut it with a knife.
And so instead of solving the problem
by trying to be really smart or work really hard,
can we just cheat and change the rules?
I think that's a better approach.
So one approach is to do what folks here like to do,
just start over.
You can't actually get rid of this problem,
but you can reset the clock on it.
Just build a new one.
Start from the beginning.
Everything's easy in the beginning.
It's only when you have users and features
that you have complexity.
So make a new programming language.
Start a new VM.
It's good.
You can't really change this long-run pressure.
But genuinely, you can reset the clock.
And I think that's part of why things like Excel
are popular and successful is they
don't have package managers.
Every time you make a new Excel document,
it's a brand new universe with none of the misery or mistakes
that you made before.
It's like the forgiveness of the blank page.
And there's something to that.
I went to a talk by John Romero at Strangeloop
not that long ago.
And he talked about how id Software had been making
these shovelware games as contractors,
or the id Software team, him and Romero and Carmack,
had been making these sort of shovelware games.
And their attitude was like, well, you should just always
start from scratch.
You get really good at it.
You can be really fast.
And each time, you do a little bit better than the one before.
And we do, I think, do better.
I love learning new languages and building new ecosystems.
And I think a big part of the reason why they're successful
is because when you have a new language,
you do have the opportunity to clear away
the standard library and also just the ecosystem of ideas
and people and sort of start from a fresh starting point.
Now, this won't cure complexity in the long run.
But it can get better, at least in the midterm.
And we can get further.
So I think that's pretty cool.
And it's also pretty fun.
So I'm all for that.
Please do more of that.
And to some extent, it feels like we
live in these unbreakable regimes
where Unity rules or where the big companies, Google
and Microsoft and everybody rules.
But that's the kind of thing that's true until it isn't.
And there's this lovely quote from Ursula Le Guin
about capitalism, which is sort of the generalization
of these problems.
Capitalism was itself an invention.
And I'll just read it.
We live in capitalism.
Its power seems inescapable.
So did the divine right of kings.
And any human power can be resisted and changed
by human beings.
So we should not doubt that the environment can be changed.
The environment was created.
It will be changed.
We don't know how or when, but it is inevitable.
OK.
So you can start over.
Revolution.
Burn it down.
Or just do less.
Do less with less.
Do I have my play date?
Do people have these?
Has anybody got a play date?
Yeah, this is great.
It's black and white.
There's only one platform.
It's small.
It comes in one color.
It only has one color, black or white,
depending on how you think about it.
Doesn't have a lot of buttons.
Doesn't have much RAM.
Doesn't really have any net.
There's a little bit of networking.
And there's only one hardware platform,
so you don't have to worry about compatibility problems.
Ish.
There is the emulator, which behaves differently.
And due to sourcing problems, they
had to get a different microcontroller.
But it transpiles natively.
They're doing a really good job.
Anyway, it's a heck of a lot simpler
than building for PS5, Xbox, PC, Switch, 3DS,
all on one code base.
It is genuinely awesome.
And because it's so small, it's kind of appealing.
And when you have less scope, you
can choose to spend that energy, that complexity budget.
You can put it into polish.
And on a small platform, a small idea can shine.
So OK, well, we can't solve complexity,
but we can make things worse.
This is actually from Augmenting Human Intellect
by Engelbart in 1962.
And it's demonstrating that you can, in fact,
change people's experience with design interventions.
I said change, not improve.
So yeah, we've made things pretty bad
in terms of software development.
This is my favorite slide always to show.
This is the foundation cloud native landscape.
I always get this wrong.
This is ostensibly, I think, $20 trillion
worth of companies.
Anyway, please memorize all of this.
There'll be a quiz at the end if you want
to make a web application in 2022.
I had to zoom out the browser just
to fit it all on screen for this one.
So I'm going to talk a little bit now
about our research, which kind of ties back into this
because I think it might be interesting.
Our approach is less the kind of reboot model and more of the
maybe do a little less with less model.
And one of our sort of research interests
kind of builds on these sort of tools for thought.
A big part of what we're interested in as a research
group is not simplicity versus complexity or decentralization
or anything like that.
But we do find that we have to work in that space
because what we want are tools that we have agency over,
that we have ownership of, that are ours and can't be taken.
And so we call our research there local first software.
And the idea is basically that instead
of having to go learn that whole chart of technologies,
that you can't actually do any of that stuff
if you just run it on your computer
because that stuff's all in the cloud.
So if you want to build software that works on your computer,
not only do you not get to use all that stuff,
you don't have to use all that stuff.
And so it's sort of like simplification
like via amputation.
So we just cut off most of the cloud,
and then we build things locally.
And so we've dabbled in a bunch of different platforms
over the years.
Right now, we're building things in the browser,
but storing everything in IndexedDB.
But one of our kind of core beliefs
is that collaboration is such an important part of thinking
and making and doing that it should
be like a really fundamental part of our platforms.
And so we've been exploring technology
that allows you to build software that runs
on your computer, but then collaborates
with other people, even allowing online offline kind of cuts.
And the model underpinning that is a data structure
called AutoMerge.
It's sort of like a portable version,
JSON-like data structure.
You could think of it as like Git for your data.
I'm happy to talk at length about this stuff,
but I don't really want to harangue you
too much on our particular kind of development interests.
But it's really incredible just how
it feels to build software that's fast and simple
and runs on your computer if you, like me,
have spent the last chunk of your career
building cloud services and running things in the sky.
I had this really memorable outage
where Amazon turned off US East 1 dirty
because the generators didn't come on in a hurricane.
And we were sort of like three days
into some godforsaken system rebuild
from backups of everybody's databases.
And my coworker turns to me, and he goes,
I'm fixing computers that don't exist in a data center I've
never been to for people I've never met.
And he just had the, like, 1,000-yard stare in his eyes.
And I was like, yeah, do you need some more coffee?
Yeah.
And so in a sense, working on this stuff
is almost like penance for me, because I created all
these single points of failure.
Anyway, so let's recap a little bit of all of this.
How do we live our lives in this complicated world, right?
So complexity occurs when our systems
have internal interactions, right?
Complexity doesn't mean, oh, there's a lot of stuff.
It's when all that stuff starts to bump against each other
and cause unpredictable outcomes.
And complexity is also a natural consequence
of system incentives.
If you have a lot of people using a thing,
and you're listening to what they need,
and you're evolving as you learn more,
you're going to end up with something complex.
And better tools won't change this, right?
The complexity is a consequence of who
we are and the choices we make.
Sure, you can burn through your budget faster.
But ultimately, where your project ends up
on the complexity scale is more about how much time
and how many ideas are invested into it than anything else.
So we can't beat complexity, but we can get beaten by it, right?
And so what are our coping strategies?
Well, we can start over.
We can eradicate dependencies.
We can cut scope, do less, right?
We can simplify our architecture.
And a really big one is being conscious of and learning
to kind of identify when you're getting
into these multiplicatory environments, right?
Once you start porting things to multiple platforms
and having to build those per-platform abstractions,
how do you manage that complexity back down?
How do you isolate complexity?
And a big part of success is isolating complexity.
But I also want to give a shout out to gazing into the abyss.
And you can go for it, right?
Embrace complexity.
Harness it.
Yeah, it's a deal with an elder god,
and you may accomplish great and terrible things,
but at a great and terrible price.
Yeah, that's fine.
But when you do this, you've got to be real careful, right?
And you want to be really deliberate about how
and when you take on that complexity.
So I guess in closing, we can't solve complexity,
but we can build better software.
Or to put it in the words of cyclist Greg LeMond,
it never gets easier.
You just go faster.
And that's all.
Thank you.
```
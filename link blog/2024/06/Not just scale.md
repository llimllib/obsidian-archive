---
created: 2024-06-05T12:57:03.217Z
updated: 2024-06-05T12:57:03.217Z
---
https://brooker.co.za/blog/2024/06/04/scale.html

> It seems like everywhere I look on the internet these days, somebody’s making some form of the following argument:

> > You don’t need distributed systems! Computers are so fast these days you can serve all your customers off a single machine!

> This argument is silly and reductive.

Instead of thinking of ideas like "you don't need distributed systems" as advice, we should be thinking of them as tools in our toolbox. Something like a slightly more practical version of Brian Eno's [Oblique Strategies cards](https://botsin.space/@oblique_strategies)

![[Pasted image 20240605090108.png]]

When confronted with a new problem, if you have the pattern "break it down into microservices" but not the "build it as a single large service" pattern, you will have a poorer view of the problem and how to build a solution.

Which is what makes this article valuable: it expands on the "you do need a distributed system" pattern, giving some reasons why it might make both technical and organizational sense to build a distributed system instead of attempting to avoid it.

It's particularly valuable for touching on the organizational benefits that distributed systems present:

> Just like computer systems, organizations scale by [avoiding coordination](https://brooker.co.za/blog/2021/01/22/cloud-scale.html). The more the organization needs different pieces to coordinate with one another to work, the less it is going to be able to grow. Organizations that wish to grow without grinding to a halt need to be carefully design, and continuously optimized, to reduce unnecessary coordination. Approaches like microservices and SoA are tools that allow technical [organizations to avoid coordinating](https://brooker.co.za/blog/2022/11/22/manifesto.html) over things like data models, implementation choices, fleet management, tool choices, and other things that aren’t core to their businesses.

I have written before that similar benefits apply to teams that choose SPA applications; the front and the back end teams can be more loosely coupled than they would otherwise be, and that can sometimes have large organizational value.
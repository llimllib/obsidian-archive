A series of three posts on the Kalman filter:

1. Voiding the warranty: how the Kalman filter updates on data: https://jbconsulting.substack.com/p/voiding-the-warranty-how-the-kalman
2. Unstable systems demand fast reflexes: https://jbconsulting.substack.com/p/unstable-systems-demand-fast-reflexes
3. Is the Kalman filter just a low-pass filter? Sometimes! https://jbconsulting.substack.com/p/is-the-kalman-filter-just-a-low-pass

I would love to learn more about these filters and write an interactive toy for exploring them. 

There are good comments on the [hn post](https://news.ycombinator.com/item?id=322713510) :

> There are many ways to think about the Kalman filter. Here are a few that I like:
> * You can think of it as a Bayesian update process for linear Gaussian systems. That is: given a prior belief of the state of a system (and an uncertainty about that belief), and a measurement about the system (and uncertainty about that measurement), the Kalman filter tells you how to combine the prior with the measurement. This is very hard to do in general, but has an exact solution if your system is Linear-Gaussian. That's magical!
> * You can also think of it as a "better way to average". If I gave you two quantities that reflected some "true" value and asked you what the true value was, you would probably average them. The Kalman filter does you one better, because it tells you to average the two quantities weighted by how confident you feel about each one.


and:

> Imagine you want to know the depth of liquid in a tank you're filling up - and you've got a noisy depth gauge and a noisy flow-rate meter.

> If you merely take the mean of the last 10 depth gauge readings, your smoothed depth reading will always lag behind the true depth, being about 5 readings out-of-date.

> By fusing together the noisy depth gauge, and the noisy flow-rate meter, and a model saying how fast depth rises with flow, you can average out the noise without creating the same level of lag.

> This is useful in applications like GPS receivers - there's noise so you _do_ need filtering, but for driving through complex junctions, the last thing you want is a 5 second delay!

How they [relate to particle filters](https://towardsdatascience.com/optimal-estimation-algorithms-kalman-and-particle-filters-be62dcb5e83):

> One of the main problems of Kalman Filters is that they can only be used in order to model situations which can be described in terms of Gaussian Noises. Although, many non-gaussian processes can be either approximated in gaussian terms or transformed in Gaussian distributions through some form of transformation (eg. logarithmic, square root, etc..).

> In order to overcome this type of limitation, an alternative method can be used: Particle Filters.

[pryo](http://pyro.ai/examples/intro_long.html) looks like a very neat library
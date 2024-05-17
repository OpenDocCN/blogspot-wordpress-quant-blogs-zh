<!--yml
category: 未分类
date: 2024-05-18 06:55:35
-->

# Physics Perspective: Thinking again about time

> 来源：[http://physicsoffinance.blogspot.com/2013/07/thinking-again-about-time.html#0001-01-01](http://physicsoffinance.blogspot.com/2013/07/thinking-again-about-time.html#0001-01-01)

I have a column coming out in Bloomberg in the next few days. The topic is time -- literally -- and how to think about it. For people reading the column, I thought I'd offer some links to things I've written here before exploring the topic in more detail, and also to some original papers that explore the ideas in much greater depth.

Much of the recent research on this topic has been done by

[Ole Peters](http://tuvalu.santafe.edu/~ole/)

of the London Mathematical Laboratory and Santa Fe Institute. The gist of his overall argument is that the usual ensemble averages used to compute "expected" returns in finance and economics are, in many cases, simply wrong. This is not the correct way to make decisions in the real world. We're all used to the idea of averaging over possible outcomes, weighted by the appropriate probabilities, and asking: is the result positive or negative? If positive, then the gamble or investment is worth it, if we can accept the risk. But this is not a legitimate way of thinking, for it averages over parallel worlds, not through time -- where we actually live.

The trouble is that usual average over different outcomes mixes potential worlds in which we go broke with others in we get rich, and does this mixing all at once, immediately, so that good outcomes coming from one path cancel out bad outcomes coming from other paths. Importantly, this mixing takes the often irreversible consequences of bad outcomes (bankruptcy, for example) out of the picture. If you make hugely risky investments, this average gives you full credit for all the wonderful possible outcomes, weighted appropriately for their likelihood, which of course seems sensible. What it doesn't do is account for the very real fact that the bad outcomes may effectively wipe you out entirely and take you out of the game, making it impossible to play again -- in which case you will never get to experience those eventual big payoffs.

I've written three earlier blog posts --

[here](http://physicsoffinance.blogspot.fr/2012/11/ergodicity-biggest-mistake-in-economics.html)

,

[here](http://physicsoffinance.blogspot.fr/2012/11/why-expected-value-is-mistake.html)

and

[here](http://physicsoffinance.blogspot.fr/2012/11/why-time-matters.html)

-- exploring his idea from different angles. These give links to Peters original papers and also to some other valuable discussions of this fundamental way of thinking. One further paper of interest is

[this recent work](http://arxiv.org/abs/1209.4517)

by Peters and William Klein which looks at how the assumption of ergodicity is systematically violated by the process of geometric Brownian motion, which is of course a workhorse model in finance and economics.

I'd like to just quote one paragraph from the latter paper to make the point of how counterintuitive this stuff is. We're all very used to thinking in terms of ensemble averages. Average over all the outcomes, weighted by the appropriate probabilities, and this should give you a good handle on whether the gamble is worth taking or not. But this view is totally mistaken. Indeed, as Peters and Klein point out,

> **In Geometric Brownian Motion, it is possible for the ensemble average to grow exponentially, while any individual trajectory decays exponentially on su fficiently long time scales** [1]. Multiplicative growth is manifestly non-ergodic. But precisely the opposite is often assumed in economics, for instance in [2], p.98: "If a gamble is `favorable' from the point of view of the expectation value [ensemble average] and you have the choice of repeating it many times [time average], then it is wise to do so. For eventually, your amount of money [is] bound to increase."

That first sentence really sums up the problem. You can do the ensemble average and say, "Hey, I expect to get exponential growth! Let's go for it." Then you actually play and find you get wiped out. Try again and still get wiped out. See that everyone who plays the same game also gets wiped out. Strange. You may eventually accept that thinking in terms of parallel worlds isn't quite the right thing to do.

Of course, Peters analyses are also closely linked to the famous Kelly criterion introduced by IBM mathematician John Larry Kelly in 1956\. The theory of practical betting based on this criterion has been extensively developed by Ed Thorpe and many others. See this

[summary paper](http://www.edwardothorp.com/sitebuildercontent/sitebuilderfiles/Good_Bad_Paper.pdf)

, for example. There is a huge literature on this, and I don't in any way want to imply that people in finance have not been thinking about this. Many have. However, the failures of the expected value approach through ensembles is not appreciated widely enough.

It goes without saying, of course, that everything becomes more uncertain and complicated in the usual case from real life -- especially in finance -- where one does not know that actual probability distribution from which outcomes are being drawn. Perhaps there is no such distribution. In this cases, Thorpe and colleagues rightly counsel even greater caution:

> The theory and practical application of the Kelly criterion is straightforward when the underlying probability distributions are fairly accurately known. However, in investment
> 
> applications this is usually not the case. Realized future equity returns may be very different from what one would expect using estimates based on historical returns. Consequentlypractitioners who wish to protect capital above all, sharply reduce risk as their drawdown increases
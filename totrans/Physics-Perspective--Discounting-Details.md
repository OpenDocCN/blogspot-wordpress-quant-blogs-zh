<!--yml
category: 未分类
date: 2024-05-18 07:06:17
-->

# Physics Perspective: Discounting Details

> 来源：[http://physicsoffinance.blogspot.com/2011/07/discountingdetails.html#0001-01-01](http://physicsoffinance.blogspot.com/2011/07/discountingdetails.html#0001-01-01)

This post offers some further details in connection with

[an essay I've written](http://www.bloomberg.com/news/2011-07-28/einstein-on-wall-street-time-money-continuum-commentary-by-mark-buchanan.html)

for

[Bloomberg Views](http://www.bloomberg.com/view/)

. It

~~will be~~

was published

~~tomorrow,~~

28 July 2011\. The topic is economic discounting, which

[I've posted on before](http://physicsoffinance.blogspot.com/2011/05/deep-discounting-errors.html)

. I naturally didn't get into any mathematical details in the Bloomberg essay, but some readers may find that looking at a little of the mathematics may help to clarify the key point of the argument. So here goes (in a sketch; I encourage everyone to read the

[original paper](http://cowles.econ.yale.edu/P/cd/d17a/d1719.pdf)

):

Suppose that the true discount rate for next year is r

[1]

, for the year after is r

[2]

, and so on, the rate for the i

^(th)

year being r

[i]

. No one knows what these will be; the rates will fluctuate from year to year. To calculate the total discount factor over a string of N years, you should multiply the individual factors associated with each year as follows,

where δt = 1 year.

But because the future isn't known, Farmer and Geanakoplos point out, determining the correct discount factor to use over the coming N years means averaging over all possible future paths, i.e. all possible sequences of values r

[1]

, r

[2]

, ... up through r

[N]

. Hence, we need to calculate the value of an "effective" discount factor given by the formula,

[Note: This sum, of course, should be divided by the total number of paths to give the average, effective discount.]

Now, it is tempting to think that when you go through the details of calculating this average, summing up the contributions for all possible paths, and dividing by the number of paths, you will find some kind of simple result in which D

[eff]

(T) will be equal to a single exponential factor with an average discount rate for the N years, r

[avg]

. In others words, you might think -- and most peoples' intuition would tend this way -- that you would find an equation such as

That is, the effective discount rate over N years takes an exponential form with some constant r

[avg]

.

Seems sensible, but turns out to be totally wrong. If you demand the equality reflected in the previous equation, then, to make it work as T gets large, it turns out that in many cases r

[avg]

will not be a constant in time, but will take on smaller and smaller values as T gets larger. This is what Farmer and Geanakoplos have shown using computer simulations to do the calculation. They used a so-called geometric random walk for the fluctuating rate r, this being the most common mathematical process used in finance to model interest rate fluctuations (i.e. this isn't a crazy or weird model, but a highly plausible one).

Their simulations show that, as a result, the effective discount factor D

[eff]

(T) doesn't have an exponential form at all, but rather a very different "power law" form,

where

α and β

are constants. This falls off with increasing T much slower than an exponential. In other words, it makes discounting much weaker than the incorrect exponential form would suggest it should be.

In the earlier post I discussed some of the implications of this result and a table indicating just how rapidly, after 200 years or so, the exponential and power law forms give wildly different results, with the exponential discounting the value of the future millions or billions of times too strong.

It's rather frightening that a subtle error could make us mis-value the future so profoundly, but this indeed seems to be what we are currently doing. The incorrect exponential form is in wide and standard use by economists doing cost-benefit analyses of everything.
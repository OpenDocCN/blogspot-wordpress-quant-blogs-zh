<!--yml
category: 未分类
date: 2024-05-12 18:56:07
-->

# Quantitative Trading: Paradox Resolved: Why Risk Decreases Expected Log Return But Not Expected Wealth

> 来源：[http://epchan.blogspot.com/2017/05/paradox-resolved-why-risk-decreases.html#0001-01-01](http://epchan.blogspot.com/2017/05/paradox-resolved-why-risk-decreases.html#0001-01-01)

I have been troubled by the following paradox in the past few years. If a stock's log returns (i.e. change in log price per unit time) follow a Gaussian distribution, and if its net returns (i.e. percent change in price per unit time) have mean

*m*

and standard distribution

*s*

, then many finance students know that the mean log returns is

*m-s*2/2*. *

That is, the compound growth rate of the stock is 

*m-s*2/2*.*

This can be derived by applying Ito's lemma to the log price process (see e.g.

[Hull](http://amzn.to/2m8SO5w)

), and is intuitively satisfying because it is saying that the expected compound growth rate is lowered by risk ("volatility"). OK, we get that - risk is bad for the growth of our wealth.

However, let's find out what the expected price of the stock is at time

*t*

. If we invest our entire wealth in one stock, that is really asking what our expected wealth is at time

*t*

. To compute that, it is easier to first find out what the expected log price of the stock is at time

*t*

, because that is just the expected value of the sum of the log returns in each time interval, and is of course equal to the sum of the expected value of the log returns when we assume a geometric random walk. So the expected value of the log price at time

*t*

is just

*t*

* (

*m-s*2/2

). But what is the expected price (not log price) at time

*t*

? It isn't correct to say exp(

*t*

 * (

*m-s*2/2

)), because the expected value of the exponential function of a normal variable is not equal to the exponential function of the expected value of that normal variable, or E[exp(x)] !=exp(E[x]). Instead, E[exp(x)]=exp(μ

*+*

σ

2/2

) where μ and σ

are the mean and standard deviation of the normal variable (see

[Ruppert](https://www.amazon.com/Statistics-Data-Analysis-Financial-Engineering/dp/1493926136/ref=as_sl_pc_qf_sp_asin_til?tag=quantitativet-20&linkCode=w00&linkId=WFSJHXJMFNABLDOT&creativeASIN=1493926136)

). In our case, the normal variable is the log price, and thus μ=

*t*

 * (

*m-s*2/2

), and σ

2

=

*t*

 *

*s*2 

. Hence the expected price at time

*t*

is exp(

*t*

*

*m*

). Note that it doesn't involve the volatility 

*s.*

Risk doesn't affect the expected wealth at time

*t*

. But we just argued in the previous paragraph that the expected compound growth rate

*is*

lowered by risk. What gives?

This brings us to a famous recent 

[paper](http://aip.scitation.org/doi/full/10.1063/1.4940236)

by Peters and Gell-Mann. (For the physicists among you, this is

*the*

Gell-Mann who won the Nobel prize in physics for inventing quarks, the fundamental building blocks of matter.) This happens to be the most read paper in the Chaos Journal in 2016, and basically demolishes the use of the utility function in economics, in agreement with John Kelly, Ed Thorp, Claude Shannon, Nassim Taleb, etc., and against the entire academic economics profession. (See

[Fortune's Formula](http://amzn.to/2mtn39y)

for a history of this controversy. And just to be clear which side I am on: I hate utility functions.) To make a long story short, the error we have made in computing the expected stock price (or wealth) at time

*t*

, is that the expectation value there is ill-defined. It is ill-defined because wealth is not an "ergodic" variable: its finite-time average is not equal to its "ensemble average". Finite-time average of wealth is what a specific investor would experience up to time

*t*

, for large 

*t*

. Ensemble average is the average wealth of many millions of similar investors up to time 

*t*

. Naturally, since we are just one specific investor, the finite-time average is much more relevant to us. What we have computed above, unfortunately, is the ensemble average.  Peters and Gell-Mann exhort us (and other economists) to only compute expected values of ergodic variables, and log return (as opposed to log price) is happily an ergodic variable. Hence our average log return is computed correctly - risk

*is*

bad. Paradox resolved!

===

**My Upcoming Workshops**

May 13 and 20:

[Artificial Intelligence Techniques for Traders](http://epchan.com/workshops)

I will discuss in details AI techniques as applied to trading strategies, with plenty of in-class exercises, and with emphasis on nuances and pitfalls of these techniques.

June 5-9:

[London in-person workshops](http://www.technicalanalyst.co.uk/courses/calendar/)

I will teach 3 courses there: Quantitative Momentum, Algorithmic Options Strategies, and Intraday Trading and Market Microstructure.

(The London courses may qualify for continuing education credits for CFA Institute members.)
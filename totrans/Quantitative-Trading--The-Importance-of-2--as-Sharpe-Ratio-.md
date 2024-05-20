<!--yml
category: 未分类
date: 2024-05-12 19:00:13
-->

# Quantitative Trading: The Importance of 2 (as Sharpe Ratio)

> 来源：[http://epchan.blogspot.com/2012/11/the-importance-of-2-as-sharpe-ratio.html#0001-01-01](http://epchan.blogspot.com/2012/11/the-importance-of-2-as-sharpe-ratio.html#0001-01-01)

A reader 

[ezbentley](http://epchan.blogspot.com/2010/04/how-do-you-limit-drawdown-using-kelly.html?showComment=1352433899601#c2233375091631222369)

recently pointed out a little-noticed fact in the

[derivation](http://www.edwardothorp.com/sitebuildercontent/sitebuilderfiles/KellyCriterion2007.pdf)

of Kelly's formula: if we apply the optimal Kelly leverage, then the standard deviation of the annualized

*compounded*

growth rate of your equity is none other than the Sharpe ratio (Sdev=S). This fact is of mild interest in itself, but its implication has relevance to another interesting fact of behavioral finance, so I will reproduce our discussions here.

Suppose our strategy has an annualized Sharpe ratio of 2\. According to the above result, Sdev=2 as well. This may startle some of us: a standard deviation of 200% of our compounded growth rate g - wouldn't ruin be very likely? But check out g itself: g=S^2/2, so g=2 when S=2, which means that g itself is exactly 200%. A Sdev of 200% here means that if the growth rate drops one standard deviation below its mean, we will still manage not to lose money for the year. Another way to put this is that there is a 84.1% chance that our annual return will be greater than 0, based on the Gaussian distribution.

It gets better if S goes above 2\. For example, at S=3, g=4.5, but Sdev is just 3\. So you can see that as S goes above 2, a 1 standard deviation fluctuation of g below the mean will still get you a positive number: profitable for the year.

This is a very interesting result: this means that S=2 is really an important threshold in more ways that I realized. From behavioral finance experiments, we already know that humans demands $2 profits for $1 risk. Given the universal desire of portfolio managers not to lose money on the year, it turns out that the demand of a Sharpe ratio of at least 2 is quite rational!

===

Now, time for a couple of public service announcements:

1) Those who are looking for a way to connect Matlab to Interactive Brokers should check out

[undocumentedmatlab.com](http://undocumentedmatlab.com/ib-matlab/)

. The creator of this product has an accompanying book, and the documentation for the product is excellent.

2)

[NAG](http://www.nag.com/numeric/MB/manual64_23_1/pdf/GENINT/product.html)

sells high performance Matlab toolboxes for those who prefer alternatives to the native ones.

3)

[Here](https://twitter.com/FIXGlobalOnline)

is the Twitter feed for FIXGlobal Online, the magazine from the creator of the FIX Protocol, an order submission standard. Interesting breaking news from the global finance scene.
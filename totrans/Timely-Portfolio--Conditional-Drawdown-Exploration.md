<!--yml
category: 未分类
date: 2024-05-18 15:06:31
-->

# Timely Portfolio: Conditional Drawdown Exploration

> 来源：[http://timelyportfolio.blogspot.com/2012/05/conditional-drawdown-exploration.html#0001-01-01](http://timelyportfolio.blogspot.com/2012/05/conditional-drawdown-exploration.html#0001-01-01)

After reading [Strub, Issam S., Trade Sizing Techniques for Drawdown and Tail Risk Control (May 21, 2012)](http://ssrn.com/abstract=2063848), I thought I should try to tie this with 2 other good R pieces on Conditional Drawdown:

> [http://systematicinvestor.wordpress.com/2011/11/01/minimizing-downside-risk/](http://systematicinvestor.wordpress.com/2011/11/01/minimizing-downside-risk/)
> [http://www.rinfinance.com/agenda/2010/Carl+Peterson+Boudt_Tutorial.pdf](http://www.rinfinance.com/agenda/2010/Carl+Peterson+Boudt_Tutorial.pdf)

As always, NONE OF THIS IS INVESTMENT ADVICE.

In Strub’s paper, he uses conditional drawdown (CDaR) and conditional VaR (CVaR) to calculate the position size on directional (breakout determined) long/short currency positions.  The results were interesting enough to attempt to replicate with slight changes.  For this post, I will use CDaR to determine the position size on a long-only [Mebane Faber 10-month moving average strategy](http://www.amazon.com/s/ref=nb_sb_noss_1?url=search-alias%3Daps&field-keywords=mebane+faber).  We will start with an efficient frontier comparison and then abandon the frontier for a systematic approach.

*(The blue text represents the added explanation in response to a comment)*

If we look below at the frontier plots of return versus each measure of risk—the most common standard deviation, CDaR (conditional drawdown), and CVaR (conditional variance at risk)—we see that the frontiers are not noticeably different.  Visually, the most different and in a bad way, is the red CVaR line in the top left frontier plot.  The red CVaR line offers less return for each unit of standard deviation than the other two frontier lines, but the underperformance is not apparent when we use CDaR or CVaR on our x-axis as our measure of risk.

Like the frontier plots above, the transition maps show only slightly different efficient allocations for each potential unit of risk.  At the lower end of the risk axis (left on the chart), we can see the biggest differences between allocations.

The lack of noticeably different results seems consistent with well-known issues of mean-variance optimization.  These issues are described very well in [this Morningstar piece.](http://corporate.morningstar.com/ib/html/pdf.htm?../documents/MethodologyDocuments/ResearchPapers/RobustAssetAllocation.pdf)

> “It is well known that mean-variance optimization is very sensitive to the estimates of returns, standard deviations, and correlations (see Michaud [1989] and Best and Grauer [1991]). Of these three inputs, returns are by far the most important and, unfortunately, the least stable. Chopra and Ziemba [1993] estimated that at a moderate risk tolerance level, mean-variance optimization is 11 times more sensitive to estimation error in returns relative to estimation error in risk (variance) and mean-variance optimization is two times more sensitive to estimation error in risk (variance) relative to estimation error in covariances (which also applies to correlations). Richard Michaud coined the phrase “the Markowitz optimization enigma” to describe the problem of input sensitivity and the highly concentrated asset allocations that result (see Michaud [1989]).
> 
> Input sensitivity indicates that the model’s output (the asset allocations) changes significantly due to small changes in the input (the capital market assumptions). Estimation error refers to the fact that in a forward-looking context the inputs are forecasts, and as such, are likely to be less than perfect (i.e. they contain errors). Putting these two issues together enables an uninformed practitioner to do more harm than good.”

For one more look at the lack of significant difference, let’s look at the cumulative returns of the 25th allocation from each efficient frontier.

Even though the frontiers for the entire period are not significantly different, we can still use these more sophisticated risk measures in a different way to determine position size.  As a simple example similar to the example provided in [Strub](http://ssrn.com/abstract=2063848), let’s say we would like to pursue a Mebane Faber style 10-month moving average style long only position in each of the 3 currencies.  We would also like to limit the CDaR of each position to be 5%, so if we are fully allocated the sum of the 3 CDaR will be 15%. We will try to achieve this by using the 12 month rolling CDaR as our expected CDaR in the next month. Here is the chart of the 12 month rolling CDaR.

If we just allocated 100% of the portfolio for each currency that exceeded its 10-month moving average, the results would look like this. Our maximum leverage across the portfolio would be 300%.

However, if we would like to allocate more than 100% in quiet times and constrain our CDaR in volatile times, we can adjust our allocation by the 12 month rolling CDaR. As an example, if the New Zealand Dollar has a 15% CDaR for the last 12 months and we want 5% CDaR, we could allocate 33% or 15%historical/5%target to the New Zealand Dollar. This could result in a near infinite position size when CDaR is small, so we could also say that we want our maximum allocation to a single currency to be 200% or 600% at a portfolio level. The cumulative return chart would look like this.

I think it very unlikely that this would be a final allocation mechanism, and I certainly would not be comfortable with this, but I hope it offers some instructive building blocks upon which you can build an allocation system.

[R code from GIST:](https://gist.github.com/2844444)
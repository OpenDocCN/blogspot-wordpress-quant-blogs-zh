<!--yml
category: 未分类
date: 2024-05-18 15:06:23
-->

# Timely Portfolio: Evaluation of Tactical Approaches

> 来源：[http://timelyportfolio.blogspot.com/2012/06/evaluation-of-tactical-approaches.html#0001-01-01](http://timelyportfolio.blogspot.com/2012/06/evaluation-of-tactical-approaches.html#0001-01-01)

Tactical approaches are often chosen based on the best cumulative return which implicitly incorporates significant hindsight bias.  Just because an approach dominates for a period of time does not indicate that it will be the best approach.  As the investment community abandons buy-and-hold and embraces tactical allocation, my guess is that the best cumulative return gathers the most assets.

[Mebane Faber’s](http://www.mebanefaber.com/) 10-month moving average system explored in

> **[A Quantitative Approach to Tactical Asset Allocation](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=962461)**
> *Journal of Wealth Management, Spring 2007*

and further refined in his book

offers a simple method for achieving what most would deem as a good result—respectable cumulative returns with significantly less risk regardless of risk measure.  Let’s play with degrees of freedom and make slight changes to the system to see how they performed in the past.  Let’s then try to decide which approach we should pursue in the future given very incomplete information.  Once we decide, let’s then decide how confident we can be in the future result.

I will test 4 systems that are all very similar in approach:

NOT INVESTMENT ADVICE.  PLEASE DO NOT USE AS THE RESULT WILL BE LARGE AND PAINFUL LOSSES.

1.  Mebane Faber 10 month moving average
2.  Rolling Proprietary (say with a smile but don’t use emoticon) Sharpe ratio > 10 month moving average
3.  Rolling Proprietary Sharpe ratio > 0
4.  Rolling Proprietary Sharpe ratio > 6 months ago Rolling Proprietary Sharpe ratio

With a little help from the fine examples given in [Download and parse EDHEC hedge fund indexes](http://tradeblotter.wordpress.com/2012/06/04/download-and-parse-edhec-hedge-fund-indexes/), we can visualize the cumulative returns and drawdowns of each approach.  I have denoted with a line 1985 which is a time when we might have chosen approach #2 since it offered significantly better cumulative returns from 1950-1985.  However, the result after our 1985 choice was not as good as we would have expected.

Again using [Download and parse EDHEC hedge fund indexes](http://tradeblotter.wordpress.com/2012/06/04/download-and-parse-edhec-hedge-fund-indexes/), we can use some more sophisticated measure of risk.  The middle (MovAvgSharpe or approach #2) offers the lowest level of historical risk on a cumulative basis.  Even though performance lagged since its 1985 first place finish, this might encourage us to still pick this approach.

To continue our move away from cumulative return towards other statistics, we can check the distribution of the monthly changes and also some higher-moment statistics skewness and kurtosis.

Even after all this exploration, we can predict nothing.  For more confidence, we might use ttrTests (explained in posts [http://timelyportfolio.blogspot.com/search/label/ttrTests](http://timelyportfolio.blogspot.com/search/label/ttrTests "http://timelyportfolio.blogspot.com/search/label/ttrTests")), use random portfolios as advocated and explained very well by [http://portfolioprobe.com](http://portfolioprobe.com), and/or let relative strength decide as advocated and explained very well by [http://systematicrelativestrength.com/](http://systematicrelativestrength.com/ "http://systematicrelativestrength.com/").  However in 30 years, we have no idea what will do best or even what best means.

[R code in GIST:](https://gist.github.com/2897532)
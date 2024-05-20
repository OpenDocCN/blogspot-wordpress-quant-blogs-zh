<!--yml
category: 未分类
date: 2024-05-12 20:28:45
-->

# Falkenblog: More Volatility-Return Evidence

> 来源：[http://falkenblog.blogspot.com/2012/05/more-volatility-return-evidence.html#0001-01-01](http://falkenblog.blogspot.com/2012/05/more-volatility-return-evidence.html#0001-01-01)

[Robeco's David Blitz](http://www.robeco.com/com/eng/institutional_investors/investments_strategies/active_quant/low_volatility_investing.jsp)

addresses the low-vol anomaly by looking at an alternative to the Fama-French 3 factor model that basically assumes equity managers are all benchmarking (see

[Agency-Based Asset Pricing and the Beta Anomaly](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=2068535#captchaSection)

). If true, the relevant metric of risk is not total return volatility, but rather benchmark volatility, where the benchmark is the market. He calls this an 'agency based model' because the standard

[principal-agent problem](http://en.wikipedia.org/wiki/Principal%E2%80%93agent_problem)

here is the investor (principal) gives money to the portfolio manager (agent), who then invests with his perverse benchmark concerns. There is a lot of anecdotes and data to suggest that institutional portfolio managers are evaluated based on their benchmark volatility, regardless of what investors truly believe, so this isn't a very radical assumption.

 Using CRSP data, and the standard 25 size-book/market Fama-French portfolios that are traditionally used for testing theory modifications, he uses monthly data generates mean 'alphas' for these portfolios, which are intercepts that theoretically should be zero (because everything else is 'in' the models). Using t-stats and joint F-tests one can assess which approach fits the data better, and the agency based model works better (as usual, there are several other tests). 

This should come as no big shock because the F-F 3-factor model assumes beta 'works', when we know it does not. Adding it was rationalized by

[Fama-French in 1993](http://www.sciencedirect.com/science/article/pii/0304405X93900235)

because it explained why equities had higher returns than bonds, and more importantly, if we admit beta is a sham most of the edifice of modern finance needs a major overhaul, not a tweak.

 Blitz's paper shines light on another angle.

[Clarke, de Silva and Thorley (2010)](http://www.iijournals.com/doi/abs/10.3905/jpm.2010.36.2.052)

introduced a volatility factor (VMS--Volatile Minus Stable), that like the momentum factor, is just a long-short portfolio that reflects the 'risk premium' to the 'volatility factor', though here this risk premium is negative so this is like an insurance premium. Adding this VMS factor to the Fama-French 3-factor model does worse than Blitz's agency-based model. Its a good think if we can quit adding anomalies to our 'risk factors' as a way of explaining them, and this research supports that effort.

 My question always was that if the standard model is correct in than beta explains why equities are riskier than bonds but does not explain returns within equities, this implies everyone holding higher-than-average beta stocks is either deluded or not in an equilibrium. The solution seemed like a duct-tape patch to a major problem, but somehow leads to no consternation at the inconsistency. Common sense is having a feel for which inconsistencies are fatal and which are noise, and my Spider-sense has always told me this is a bad inconsistency.

 Meanwhile, there is a lot of research out there on this issue that

[makes me go hmm](http://www.youtube.com/watch?v=XF2ayWcJfxo)

, because their numbers are so different than what I see looking at the same data. For example some

[researchers at the EDHEC Business school](http://www.edhec-risk.com/edito/RISKArticleEdito.2011-09-20.1606)

came out with a paper showing that returns fall if you look at a 1-month horizon, but rise pretty consistently when you looked over a 24-month holding period. I don't see how they got this, but suspect it has something to do with their inclusion requirements, such as including only stocks that existed over the subsequent 24 months. Further, they had no size exclusions, so they probably used every little penny stock that generates outsized returns but was non-tradable as a practical matter. I'm just guessing, because I don't see how they got such a large volatility premium (they used several to the same effect).

From *Is there a risk/return trade-off across stocks? *

Table 1: Geometric mean returns for multi-portfolio analysis. July 1963 to December 2009.

On the other side, recently the self-proclaimed 'father of low vol investing' Bob Haugen and his loyal co-author Nardin Baker have quintuple-downed on standard estimates of the anomaly.  In

[Low Risk Stocks Outperform within All Observable Markets of the World](http://www.lowvolatilitystocks.com/bob-haugen-index2/low-risk-stocks-article/)

, with a downloadable spreadsheet, they find a whopping

**19% annualized return differential**

between the lowest and highest volatility deciles in the US from 1990-2011.

I think Haugen and Baker have the sign right, as opposed to the EDHEC group. Yet I also think they overclubbed it by a factor of 5\.
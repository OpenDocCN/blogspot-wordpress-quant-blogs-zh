<!--yml
category: 未分类
date: 2024-05-18 15:02:45
-->

# Timely Portfolio: Drawdown Determined Position Size

> 来源：[http://timelyportfolio.blogspot.com/2012/11/drawdown-determined-position-size.html#0001-01-01](http://timelyportfolio.blogspot.com/2012/11/drawdown-determined-position-size.html#0001-01-01)

This caught my eye as I searched for some more academic research on my favorite risk measure drawdown.

> Yang, Z. George and Zhong, Liang, *Optimal Portfolio Strategy to Control Maximum Drawdown -
> The Case of Risk Based Dynamic Asset Allocation* (February 25, 2012).
> Available at SSRN: [http://ssrn.com/abstract=2053854](http://ssrn.com/abstract=2053854) or [http://dx.doi.org/10.2139/ssrn.2053854](http://dx.doi.org/10.2139/ssrn.2053854)

The paper seeks to do what I have tried to do without any real success—use drawdown to help determine position size.  I felt motivated to replicate in R their measure Rolling Economic Drawdown-Controlled Optimal Portfolio Strategy (REDD-COPS).  Since drawdown suffers from a significant lag, the authors suggest a rolling drawdown to offset some of the embedded lag:

> "Intuitively, a drawdown look-back period H [length of rolling period] somewhat shorter than or similar to the market decline cycle is the key to achieve optimality. Substituting EDD with a lower REDD in equation (1), we have higher risky asset allocation to improve portfolio return
> during a market rebound phase. In the examples followed, we'll use H = 1 year throughout."

The authors calibrate REDD-COPS on the S&P 500 as a single asset, and then use REDD-COPS in a portfolio context with three assets (S&P 500 – SPY, US 20+ Year Treasury – TLT, and DJ UBS Commodity Index).  I’ll show the results from my attempt to replicate the single asset test.  Sorry for the Thanksgiving but ugly colors, but I just could not resist.

Their results are interesting, but I’m not entirely convinced of the robustness of a system using REDD-COPS to determine position size especially since their use of entire period Sharpe requires hindsight.  However despite the ultimate result, the byproduct discovery discussed in my post [Cash–Opportunity Lost or Opportunity Gained](http://timelyportfolio.blogspot.com/2012/11/cashopportunity-lost-or-opportunity.html) was well worth the effort.  Stay tuned for my attempt to do the multi-asset REDD-COPS system.

[R code in GIST:](https://gist.github.com/4115759)
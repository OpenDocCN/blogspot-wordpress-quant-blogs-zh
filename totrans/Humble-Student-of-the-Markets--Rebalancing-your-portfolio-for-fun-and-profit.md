<!--yml
category: 未分类
date: 2024-05-18 03:28:56
-->

# Humble Student of the Markets: Rebalancing your portfolio for fun and profit

> 来源：[https://humblestudentofthemarkets.blogspot.com/2014/11/rebalancing-your-portfolio-for-fun-and.html#0001-01-01](https://humblestudentofthemarkets.blogspot.com/2014/11/rebalancing-your-portfolio-for-fun-and.html#0001-01-01)

This is part two of a two part post on portfolio rebalancing (see

[How to rebalance your portfolio (NAAIM maniac edition)](http://humblestudentofthemarkets.blogspot.com/2014/11/how-to-re-balance-your-portfolio-naaim.html)

for part one).

The standard practice among portfolio managers is to establish a rebalancing discipline for their portfolios. A typical process would involve the following steps:

1.  Determine the target asset mix, which could change depending on market conditions.
2.  Re-balance if:

*   The asset mix weights moves more than a certain percentage, e.g. 10%, from the target weight; or
*   Periodically, e.g. on an annual basis

These are all sensible rules that have long been practiced in the investment industry. In essence, the strategy involves taking profits on winning asset classes and averaging down on losers as a form of risk-control discipline.

Then I came upon an intriguing paper by Granger, Greenig, Harvey, Rattray and Zou entitled 

[Rebalancing Risk](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=2488552)

. Here is the abstract:

> While a routinely rebalanced portfolio such as a 60-40 equity-bond mix is commonly employed by many investors, most do not understand that the rebalancing strategy adds risk. Rebalancing is similar to starting with a buy and hold portfolio and adding a short straddle (selling both a call and a put option) on the relative value of the portfolio assets. The option-like payoff to rebalancing induces negative convexity by magnifying drawdowns when there are pronounced divergences in asset returns. The expected return from rebalancing is compensation for this extra risk. We show how a higher-frequency momentum overlay can reduce the risks induced by rebalancing by improving the timing of the rebalance. This smart rebalancing, which incorporates a momentum overlay, shows relatively stable portfolio weights and reduced drawdowns.

**Monthly rebalancing does the worst**

You would think that, for example, given the massive losses seen during the Lehman Crisis episode, that a rebalanced portfolio where the investor bought all the way down would see superior returns. Interestingly, that was not the case.

In the paper, the authors compare and contrast a simple drift weight strategy, i.e. not rebalancing at all, with a fixed weight monthly rebalancing strategy. The chart below shows how that the monthly rebalanced portfolio actually showed a higher risk profile than the passive drift portfolio. (There were other examples in the paper, but I will focus on this period for the purpose of this post).

By contrast, they advocate a partial momentum strategy. In essence, this amounts to the application of of a trend following system to rebalancing. The idea is, as the stock market goes down and the bond market goes up, you keep overweighting your winners (bonds) and don't rebalance the portfolio until momentum starts to turn. As the chart below shows, the portfolio with the partial momentum overlay performed better than either the monthly rebalanced or passive drift weight portfolio.

**Talking their book?**

These are intriguing results and a demonstration of the positive effects of using trend following techniques for portfolio construction. However, I would add a couple of caveats in my read of this paper.

First, three of the five authors work for MAN Group, which is known for using trend following techniques in their investing. While this paper does show the value of these kinds of techniques, I am always mindful that researchers may be "talking their own book". As regular readers are aware, I extensively use trend following models in my own work, but I am cognizant of the weaknesses of these models.

In particular, these models perform poorly in sideways choppy markets with no trends. As an example, consider this chart of sugar prices for the period from 1891 to 1938\. Unless the trend following system is properly calibrated, the drawdowns using this class of model are potentially horrendous.

As another example, try wheat prices for the 1872 to 1944 period:

A second critique of the approach used by the paper is the use of monthly rebalancing as one of the benchmarks. In practice, no one rebalances their portfolio back to benchmark weight on a monthly basis. A more realistic rebalancing technique might be a rule based rebalancing approach of rebalancing either annually or if the portfolio weights drift too far from the policy benchmark.

To be fair, however, the monthly rebalancing approach is an extreme one that does differentiate between a passive drift weight and a more frequently rebalanced portfolio.

**Value vs. Momentum**

In summary, this is an intriguing paper that compares and contrasts the use of price momentum, or trend following, techniques of chasing winners to a value-based rebalancing strategy of buying assets when they are down.

Before going out and blindly implementing a trend-following based re-balancing program, I urge portfolio managers to further study these approach and adopt it to their own circumstances. Your mileage will vary.
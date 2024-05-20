<!--yml
category: 未分类
date: 2024-05-12 17:40:55
-->

# When Should You Buy Momentum? Mean-Reversion in The Momentum Factor | CSSA

> 来源：[https://cssanalytics.wordpress.com/2019/09/12/when-should-you-buy-momentum-mean-reversion-in-the-momentum-factor/#0001-01-01](https://cssanalytics.wordpress.com/2019/09/12/when-should-you-buy-momentum-mean-reversion-in-the-momentum-factor/#0001-01-01)

Recently there was a [good post](https://www.bespokepremium.com/interactive/posts/think-big-blog/momentum-massacre) by Bespoke Research highlighting the “Momentum Massacre” that we recently witnessed in the market. High- flying momentum stocks were decimated and the low momentum/losing stocks made a roaring comeback. One of the best ways to track the momentum factor is to look at the ETF ticker symbol: [MOM or QuantShares U.S. Market Neutral Momentum Fund](https://www.agf.com/us/products/mom/index.jsp). As you can see in the chart below, the momentum factor has taken the elevator down over the past 10-days completely reversing total returns year to date.

![](img/84be003a26c9adfcfdffd9ba720e4624.png)

This begs the obvious question: can we expect some mean-reversion in performance going forward? As a simple test I took a look at 10-day returns in MOM and smoothed them using a 5-day average to account for some of the noise in closing prices for less liquid ETFs. Then I took the cumulative percentile ranking looking at all data available at each point-in-time of that smoothed 10-day return. What I found was that in the last 8 years (the maximum data available), the momentum factor has been highly mean-reverting. If you bought the momentum factor after smoothed 10-day returns were above the median (.5) you lost money consistently. In contrast if you bought when returns were below the median you made money consistently. Clearly mean-reversion has been a powerful factor driving performance as you can see in the chart below:

![](img/8ae5a19211f9a76b56f4c9d4eff589da.png)![](img/baca4602782dc180dc4c73aee63af905.png)

To get a sense of how this would benefit investors that follow high momentum stocks, I looked at how using the same mean-reversion oscillator on MOM could be used to time [MTUM or iShares MSCI USA Momentum Factor](https://www.ishares.com/us/products/251614/ishares-msci-usa-momentum-factor-etf). In the chart below we see that using this oscillator has been a very useful way to time whether to be in or out of high momentum stocks:

![](img/8464ea75a1a314c2614e2ff4bc4dee42.png)![](img/5bf78276c82945b9a7ff0f8105863e47.png)

When the momentum factor was oversold (<.5) you made almost 17% annualized with a sharpe of 1.74, and in contrast when the momentum factor was overbought- which was nearly 50% of the time- you lost money. One of the obvious questions is whether there is some bias in the momentum methodology unique to MTUM that makes it less generalizable to a more concentrated approach. To address this concern I tested using the oscillator on [QMOM or Alpha Architect’s U.S. Quantitative Momentum ETF](https://etfsite.alphaarchitect.com/qmom/). While there is a much shorter history the general conclusion is the same: mean-reversion in the momentum factor is a good way to time momentum stocks:

![](img/8f80039c03d87cd902a45a1c6f90dbb2.png)

Finally, and perhaps the most interesting test was whether or not the momentum factor on stocks can be used to time asset class momentum. I have read studies in the past that show that the momentum factor is correlated to asset class momentum. If that is the case then we can expect that the oscillator should be effective in timing global asset allocation. To test this I used [GMOM or Cambria’s Global Momentum ETF](https://www.cambriafunds.com/gmom). The chart tells the story below:

![](img/a751dcb408f4e621d32a124021968511.png)

Clearly mean-reversion has been effective for timing global asset allocation that uses a momentum approach. What was surprising was just how effective it was. Having more data using proxy strategies to test these hypotheses over a larger sample size would be valuable, but I currently don’t have access to that data on a daily basis going far back in time. Nevertheless, it is still very important to respect current market trends and how they impact investment strategies. In recent times, the effect of mean-reversion in momentum factor is a very real and material driver of performance.

Why might there be a mean-reversion effect in the momentum factor? I think that a lot of stat arb money chases the momentum factor, and to be able to rebalance in order to maintain risk limits and to unwind positions they need to sell when they are profitable and buy back when they are losing money. To do so requires that a lot of retail and other institutional money be chasing or fleeing from momentum in order to provide them with liquidity. Perhaps this “smart money” effect explains why momentum is mean-reverting. In either case trying to explain why this happens would require a very thoughtful and deep analysis in the form of a serious research paper.
<!--yml
category: 未分类
date: 2024-05-18 14:01:38
-->

# Rotation System à la Quantum Financier – Quantum Financier

> 来源：[https://quantumfinancier.wordpress.com/2010/11/11/rotation-system-a-la-quantum-financier/#0001-01-01](https://quantumfinancier.wordpress.com/2010/11/11/rotation-system-a-la-quantum-financier/#0001-01-01)

Rotation systems have generated a lot of virtual ink lately see CSS Analytics [here](http://cssanalytics.wordpress.com/2010/02/23/rotation-concepts/), Engineering Returns [here](http://engineering-returns.com/2010/07/23/rotational-trading-a-simple-but-powerful-concept-part-i-ii/), then at MarketSci [here](http://marketsci.wordpress.com/2010/10/20/roundup-tactical-asset-allocation/) for a few examples. I have recently been playing around with the concept but with a very different approach. I figured it might be interesting for readers to hear another approach to a similar problem.

Rotation systems are often based on two very simple concepts: momentum (relative strength) effect and negative correlation. The goal of such models is usually to allocate capital to securities trending on the upside. By selecting securities that are show negatively correlated behaviour we expect the securities to complement each other depending on the regime. For example one could include in the basket of available securities stocks and fixed incomes ETFs with the expectation to be long bond when stocks are not performing and vice-versa. This kind of model basically surfs the beta with the momentum of securities. This approach demands certain considerations when creating the model, and depending on the investor, various degrees of fancy maths are going to be used. When looking at creating such systems, we need to determine the following amongst others:

**1\. What securities are available and how are they selected?**
The negative correlation amongst assets is a desirable feature here. We possibly also could include ETFs with different degrees of leverage to aggressively add beta when the time is right. Then we can select them based on heuristic, macroeconomic relationship, data mining etc.

**2\. How is momentum measured and ranked?** It could be using a simple normalized difference between prices of different time frames or a rate-of-change indicator. The RSI , [DVO](http://cssanalytics.wordpress.com/2009/07/29/the-dvo/) or [TSI](http://engineering-returns.com/tsi/) indicators are also good candidates. Alternatively you could fit a least square model and evaluate slope and residuals. You could also do some kind of factor decomposition and create a factor model to forecast momentum.

**3\. How do we allocate capital across securities?** A simple equal cash position could be used or we could use volatility to adjust the weight amongst securities. Mean-variance optimization with certain tweaks to it would perhaps make a good candidate.

**4\. How often do we recalibrate the strategy?** Most TAA systems recalibrate monthly and some rotation systems trade on a weekly time frame. The trick is to minimize the transaction cost while still capitalizing on the uptrend of selected securities and mitigating the drawdown. The appeal of such systems is usually their risk adjusted performance and we would not want to compromise it.

**5\. Do we consider alternative/innovative metrics in the system?** Michael at Marketsci recently talked about taking correlation during market shocks into considerations. This type of innovative approach seemed to work quite well for him, and really here sky is the limit. We only have to balance complexity and quality.

Without spoiling the next post, I can say that my rotation system will be very different from anything discussed so far on the blogosphere (as far as I am aware). Instead of using historical relative strength we will see how we can use machine learning classification and select securities using the forecast. I will also try to incorporate new metrics to help with system performance.

QF
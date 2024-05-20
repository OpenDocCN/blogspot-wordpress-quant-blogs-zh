<!--yml
category: 未分类
date: 2024-05-12 18:06:04
-->

# Diversification and Risk Reduction | CSSA

> 来源：[https://cssanalytics.wordpress.com/2012/07/16/diversification-and-risk-reduction/#0001-01-01](https://cssanalytics.wordpress.com/2012/07/16/diversification-and-risk-reduction/#0001-01-01)

The concept of diversification is more nuanced and complex than most people realize. The global financial crisis today highlights serious deficiencies our true understanding of the subject. Multi-asset and large-scale risk allocation is a highly dimensional problem for which there is no closed-form solution. The integration of both qualitative and quantitative considerations are necessary in the context  of an adequate solution. As with most cases in the investment world, the approach is always polarized towards philosphical preference : Discretionary portfolio managers realize the limitations of basic numerical solutions and how to apply “common sense” to capture these deficiencies. The drawback is that they tend to substitute rules of thumb that lack rigor, accuracy, or sufficient complexity. In contrast, “quants” often fail to account for both common sense and the violation in the assumptions underlying their models that are present in real-life problems. To their credit, they use models that are far more capable of handling such complex problems in an unbiased manner.

Diversification is more than just a prescription for holding a large number of assets, it is also about the relationships between those assets, the relative risk contribution of those assets, and also possibility of a sudden large loss or default. This is by no means a complete accounting, which is beyond the scope of this post. There is a much simpler formula that is straightforward to derive from portfolio mathematics that neatly captures many of the nuances of diversification and its contribution to risk reduction in a portfolio context:

**Portfolio Variance**= K x Average Asset Variance  +(1-K) x Average Asset Covariance

where K=  1/number of assets in the portfolio

Since most people cannot easily conceptualize variances and covariances, it is easier to translate this already simplified formula into one that is more intuitive:

We first note that:

Variance= Stdev^2  or Standard Deviation Squared

Covariance= Correlation (AB) x Stdev (asset A) x Stdev (asset B)

or Correlation times the Standard Deviation Product (SDP)

the equation can be more intuitively written as:

**Portfolio Risk (Variance)**= K x (Average Standard Deviation)^2 + (1-K)x( Average Correlation x Average SDP)

What is clear from this formula is that the average standard deviation across assets is insufficient for calculating portfolio risk– but this is still not clear enough to describe the levers that drive portfolio risk. We know that actual portfolio risk is always less than the average portfolio risk across assets as long as the correlation between assets is less than perfect.  The difference can be described as the *risk reduction due to diversification*.

Risk Reduction=  Portfolio Risk (Variance)/ Average Asset Risk (Variance)-1

How do we translate the portfolio risk formula above to easily understand how risk is reduced in a portfolio format?  Lets assume  that the standard deviation of all assets are approximately the same and have a value of 20% annualized. This means that the average risk or variance is 4%. The average SDP (standard deviation product) is also equivalent to 4%  since all assets have a standard deviation of 20%. This means that the Portfolio Risk formula can easily be seen as:

**Portfolio Risk**= **K x average asset risk + (1-K) x (average asset correlation x average asset risk)**

Portfolio risk is clearly a function of  1) the average asset risk 2) the constant “K” and 3) the average correlation between assets. The constant “K” can be thought of as an inverse multiplier(1/number of assets) that weights the contribution of average asset risk  to portfolio risk as a function of the number of assets in the portfolio. The higher “K” is, the less important the average asset risk is and the more important the average correlation between assets becomes. Other things being equal, the more assets in the portfolio at a given level of average correlation will reduce risk at the portfolio level.  The constant “K” becomes quite small with even 10 assets, making the contribution of the first term of the equation less important.  In fact for large data sets with greater than 50 assets, the portfolio risk formula can actually be roughly approximated by :

**Portfolio Risk (for large datasets)**= **Average Asset Correlation x Average Asset Risk**

recall that Risk Reduction due to diversification= Portfolio Risk/Average Asset Risk-1

by substituting in our approximation for portfolio risk  we are left with the following simplification:

**Risk Reduction** (due to diversification)= **Average Asset Correlation -1**

This makes intuitive sense- to reduce portfolio risk, we need to find assets that have a low average correlation. To maximize this effect, we need to ensure that we have a lot of assets and also use assets that have similar risks (or one can create equivalent asset risks  through volatility sizing).  It is this general intuition that drives portfolio algorithms that seek to maximize diversification or minimize portfolio correlations……………….
<!--yml
category: 未分类
date: 2024-05-12 18:59:15
-->

# Quantitative Trading: Cointegration Trading with Log Prices vs. Prices

> 来源：[http://epchan.blogspot.com/2013/11/cointegration-trading-with-log-prices.html#0001-01-01](http://epchan.blogspot.com/2013/11/cointegration-trading-with-log-prices.html#0001-01-01)

In my recent 

[book](http://www.amazon.com/dp/1118460146/ref=as_li_qf_sp_asin_til?tag=quantitativet-20&camp=14573&creative=327641&linkCode=as1&creativeASIN=1118460146&adid=00W7DZWKQ8DNBM541YD6&&ref-refURL=http%3A%2F%2Fepchan.blogspot.ca%2F)

, I highlighted a difference between cointegration (pair) trading of price spreads and log price spreads. Suppose the price spread hA*yA-hB*yB of two stocks A and B is stationary. We should just keep the

**number of shares**

of stocks A and B fixed, in the ratio hA:hB, and short this spread when it is much higher than average, and long this spread when it is much lower. On the other hand, for a stationary log price spread hA*log(yA)-hB*log(yB), we need to keep the

**market values**

of stocks A and B fixed, in the ratio hA:hB, which means that at the end of every bar, we need to rebalance the shares of A and B due to price changes.

For most cointegrating pairs that I have studied, both the price spreads and the log price spreads are stationary, so it doesn't matter which one we use for our trading strategy. However, for an unusual pair where its log price spread cointegrates but price spread does not (Hat tip: Adam G. for drawing my attention to one such example), the implication is quite significant. A stationary price spread means that prices differences are mean-reverting, a stationary log price spread means that returns differences are mean-reverting. For example, if stock A typically grows 2 times as fast as B, but has been growing 2.5 times as fast recently, we can expect the growth rate differential to decrease going forward. We would still short A and long B, but we would exit this position when the growth rates of A vs B return to a 2:1 ratio, and not when the price spread of A vs B returns to a historical mean. In fact, the price spread of A vs B should continue to increase over the long term.

This much is easy to understand. But thanks to a reader Ferenc F. who referred me to a paper by

[Fernholz and Maguire](http://www.jstor.org/stable/4480875)

, I realize there is a simple mathematical relationship between stock A and B in order for their log prices to cointegrate.

Let us start with a formula derived by these authors for the change in log market value P of a portfolio of 2 stocks: d(logP) = hA*d(log(yA))+hB*d(log(yB))+gamma*dt.

The gamma in this equation is

gamma=1/2*(hA*varA + hB*varB), where varA is the variance of stock A

minus

the variance of the portfolio market value, and ditto for varB.

Note that this formula holds for a portfolio of any two stocks, not just when they are cointegrating. But if they are in fact cointegrating, and if hA and hB are the weights which create the stationary portfolio P, we know that d(logP) cannot have a non-zero long term drift term represented by gamma*dt. So gamma must be zero. Now in order for gamma to be zero, the

**covariance**

of the two stocks must be positive (no surprise here) and equal to the

**average of the variances**

of the two stocks. I invite the reader to verify this conclusion by expressing the variance of the portfolio market value in terms of the variances of the individual stocks and their covariance, and also to extend it to a portfolio with N stocks. This cointegration test for log prices is certainly simpler than the usual CADF or Johansen tests! (The price to pay for this simplicity? We must assume normal distributions of returns.)

=== My online Quantitative Momentum Strategies workshop will be offered on December 2-4\. Please visit [epchan.com/](http://epchan.com/my-workshops)[my-workshops ](http://epchan.com/my-workshops)for registration details.
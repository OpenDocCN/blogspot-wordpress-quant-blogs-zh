<!--yml
category: 未分类
date: 2024-05-12 18:36:42
-->

# Introduction to D-VaR Position Sizing (Part 1) | CSSA

> 来源：[https://cssanalytics.wordpress.com/2010/02/04/introduction-to-d-var-position-sizing-part-1/#0001-01-01](https://cssanalytics.wordpress.com/2010/02/04/introduction-to-d-var-position-sizing-part-1/#0001-01-01)

Position-sizing is the least exciting topic in trading. We all find ourselves too busy looking for the ultimate trading strategies or indicators to bother with spending time thinking about how much to bet. Contrary to what you might think, figuring out how much you should bet is not just a matter of determining your expected edge. Unlike casino games with defined odds, markets are uncertain and adjusting for the unexpected tail loss is just as important as adjusting for the  expected size of your edge.

 This concept is not new to hedge funds, and to those that trade for a living; They often think about risk first because their continued existence depends on staying in the game. For this sophisticated bunch, position-sizing, diversification, and hedging are the cornerstones of their risk management approach. Many of them are well aware that initial stop losses (in contrast to trailing stops which are very useful) are highly overrated as a means of managing risk–and if used improperly will increase your chances of going broke. This is because if they are placed too tight they will protect you from tail risk but expose you to more noise. If they are place too far the reverse is true– especially with unexpected gaps.  The tradeoff is simple:  death by one severe blow, or death by a thousand cuts. Finding the optimal balance is very difficult. Initial stops are not sufficient to manage risk by themselves and function much better when they are integrated with other risk management tools. In contrast, position sizing is very useful since you a) don’t face timing risk and b) can only lose what is invested–if you bet 5% of your portfolio no surprise gaps will lead you to losing more than you have bet. 

To the best of my knowledge, I do not believe that this particular position-sizing method has been published somewhere before. However I do know that it is based on the well-known concept of “Value-at-Risk.”  From Investopedia this is defined as follows [http://www.investopedia.com/terms/v/var.asp](http://www.investopedia.com/terms/v/var.asp):

**What Does *Value at Risk – VaR* Mean?**
A technique used to estimate the probability of portfolio losses based on the statistical analysis of historical price trends and volatilities.

**Investopedia explains *Value at Risk – VaR***
VaR is commonly used by banks, security firms and companies that are involved in trading energy and other commodities. VaR is able to measure risk while it happens and is an important consideration when firms make trading or hedging decisions.  

Generally speaking VaR looks at tail risk ,which in the industry is defined by the magnitude of expected losses at the 95th percentile (or 5% percentile of the daily P/L distribution of any strategy). Knowing the maximum losses that  might occur in extreme circumstances helps risk management professionals prepare for the worst. If you know what % risk your portfolio may incur you can theoretically budget your portfolio or individual stock position sizing to allow for a given maximum. Conventional practice is to use a normal distribution for this this task– all that needs to be known is the mean and standard deviation and this estimate can easily be derived. Unfortunately for the slide-rule boys, financial markets are really not normally distributed and tend to exhibit “fat tails.” What this means is that the maximum risk (or upside) is actually both more probable and larger than what would be expected in a utopian trading universe.  This means that typical volatility-based position sizing inherently rests on a shaky foundation. (more on this later) Why not simply look at the empirical distribution of daily returns? After all, our own empirical observation tells us that normal distributions are flawed, so why not manage risk based on experience?

In this method we will use an incredibly simple approach:

1) take the daily returns for a given stock, index or strategy

2) compute the 5th percentile of returns (max tail loss)

3) select a budgeted risk level as a maximum daily loss such as 1% (conservative) or 1.5% (aggressive)

4) your position size is the budgeted risk level divided by the absolute value of the max tail loss

5) this position may not exceed 200%

Our goals are the following:

1) Reduce the size of the worst maximum loss – especially relative to a passive buy and hold strategy

2) Improve the sharpe ratio or risk-adjusted return- also relative to a passive buy and hold strategy

The following test was done on the Dow Jones Industrial Average using Yahoo Finance data going back slightly more than 20000 bars back to 1928:

| VAR Position- Sizing DJIA 1928-Present |   |   |
|   |   |   |   |   |   |
|   | **Gross ** |  |  | **worst daily** |
|  | **Sharpe** | **CAGR** | **SD** | **loss** |   |
| Buy and Hold | 0.24 | 4.5% | 18.4% | -22.6% |   |
| D-VAR 1% risk | **0.45** | 5.2% | 11.5% | **-7.6%** |   |
| D-VAR 1.5% risk | 0.41 | **6.9%** | 16.7% | -11.4% |   |

As you can see, both goals are achieved– D-VaR shows much lower tail risk and a higher sharpe ratio. As a side bonus, it actually produces a higher CAGR than buy and hold. From the crash of 1929,the crash of 1987, the Asian crisis in 1998, to October 2008, D-Var survived them all with limited tail risk without any use of timing related tools. This makes it a definite candidate as a new position sizing method that works in real-life. In subsequent posts I will give some more examples how this can be used in basic trading strategies that are both long and short.
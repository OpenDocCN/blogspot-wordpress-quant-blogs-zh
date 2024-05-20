<!--yml
category: 未分类
date: 2024-05-12 18:11:34
-->

# Volatility Differentials: High/Low Volatility versus Close/Close Volatility (HLV-CCV) | CSSA

> 来源：[https://cssanalytics.wordpress.com/2011/03/29/volatility-differentials-highlow-volatility-versus-closeclose-volatility-hlv-ccv/#0001-01-01](https://cssanalytics.wordpress.com/2011/03/29/volatility-differentials-highlow-volatility-versus-closeclose-volatility-hlv-ccv/#0001-01-01)

I am often asked why the performance of DVB is far superior in terms of CAGR to other oscillators such as the RSI2\. My answer is simple: the volatility of intraday Highs versus intraday Lows is far more predictable and relevant than close to close volatility in the current environment. I began to notice this while trading pairs in 2008, and subsequently realized that this phenomenon existed on most heavily traded markets. What is interesting is that this has historically been relevant across major futures markets far before the halcyon of index mean-reversion that was ushered in at the turn of the millenium in 2000\.  Whether this is because of the advent of high frequency trading, a pronounced jump in program trading, or a broad decline in retail intraday volume — or all three for that matter, it is quite clear that the highs and lows set support and resistance points from which there tend to be  predictable mean-reverting bounces.

The fact that this has existed in most liquid futures markets as far back as 1985 suggests some linkage between the composition of market players and large speculative volume intraday. Perhaps such markets are geared towards taking advantage of natural tendencies in human behavior. Its easy for the leveraged futures trader to panic when prices finish near the lows of the day and be subject to overnight risk. The natural tendency would be to sell to the larger and more sophisticated market players and pay the a risk premium to avoid such risk. The opposite would be true when the market finishes near the highs, where an inexperienced speculator may choose to be risk-seeking and looking for a breakout. The speculator will pay a tax to gamble that resistance will be taken out to the large speculator or informed trader (ie Goldman or the Fed).

The fact that bull markets make most of their gains overnight –and especially if they close near their lows of the day is yet a further tax on the nervous day-trader who will not only face the smaller point ranges offered intra-day, but also has a net negative expectation.In a bear market, all of the losses are made during the day and news flow can have an unpredictable and predominantly negative influence overnight. This makes it very scary to go long–especially at the lows and risk incredible losses the next day. Furthermore the trader also learns that if they choose to stick with shorting some of the most significant gaps occur overnight on positive developments, and the next day there is a stampede to buy that starts at the open. Hence it becomes scary to short overnight. **At the end of the day the market pays you to do the things that are hard to do or counterintuitive, and this is a classic example.**

While I will not attempt to prove any of these theories in the current post, I would like to present a useful indicator that certainly supports my case that High/Low volatility is more important than Close to Close volatility. It is also valuable as a filter for mean-reversion trades regardless of whether you use close to close indicators or high/low indicators. The logic behind this indicator/filter is that there is a dynamic relationship between close to close and high minus low volatility. Furthermore in a subsequent post, I will show how to take a slightly more complicated approach to build a dynamic trading strategy to take advantage of this effect that is superior to the sum of its parts.

For now, I will present the simplest variant of **HLvol vs CCvol:**

1) take today’s high minus low and subtract the absolute value of the difference between today’s close and yesterday’s close:

raw differential= (H-L)- abs(C- C t-1)

2) take the average, in this case the 5-day or 10-day sma of the raw differential

3) when the current differential is below the average differential this indicates that volatility has contracted and is likely to expand, the reverse is true when the differential is above average.

**Note:** the net difference between today’s raw differential and the 5 or 10-day sma of the raw differential can be normalized using a z-score or a percentile ranking.
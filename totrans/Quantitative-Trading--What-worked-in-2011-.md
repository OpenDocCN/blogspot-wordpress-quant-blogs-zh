<!--yml
category: 未分类
date: 2024-05-12 19:02:09
-->

# Quantitative Trading: What worked in 2011?

> 来源：[http://epchan.blogspot.com/2012/01/what-worked-in-2011.html#0001-01-01](http://epchan.blogspot.com/2012/01/what-worked-in-2011.html#0001-01-01)

We all know that 2011 was a bad year for many hedge funds, with the average fund

[down 5%](http://online.wsj.com/article/SB10001424052970203806504577180941947811200.html)

. But what type of strategies did well, and what did particularly poorly? The numbers are out: Forex funds lose more than average, down 6%. In fact, 71 out of 77 Forex funds tracked by a Citigroup currency analyst were down in 2011\. And the winners are? Statarb funds, with a

[5% averge return](http://www.bloomberg.com/news/2012-01-10/chase-coleman-channels-ancestor-stuyvesant-with-45-robertson-like-return.html)

.

This superior performance of statarb funds is quite a contrast from the last financial crisis 2007-9\. Then, most of the big factor-driven statarb models

[failed miserably](http://epchan.blogspot.com/2007/08/readers-comment-on-quant-funds-losses.html)

. What caused this difference? Is it because the risk management techniques of big funds have improved? Or maybe that's because in 2011, the deviation from factor returns mean-revert within a few days, so those statarb models that re-balance on a daily basis can benefit from the buying/selling opportunity at steep discount/premium?

To settle this question, let me report the 2011 backtest results (without transaction costs) of running

[Andrew Lo](http://epchan.blogspot.com/2007/10/how-mean-reversion-strategy-performed.html)

's prototype mean-reversion model : ranking stocks based on their previous day's returns, shorting the top decile and buying the bottom one, rebalancing only at the close. (Click on chart to make it larger.)

The APR in 2011 was 18.6%. Note in particular its performance since the crisis began officially on 20110808: despite a steep drawdown, the overall performance was spectacular! Clearly, high volatility benefited a prototypical statarb strategy, and the out-performance has not much to do with improved risk management.

You might wonder what would happen if we had used the intraday version of this strategy instead: enter all positions at the open, and exit them all at the close? I tried it: the performance is surprisingly similar to the interday strategy. So intraday vs. interday volatility or mean-reversion does not seem to play a part in last year's equities market. Contrasting this with the performance of Forex models, it is clear that high volatilities benefited statarb models while they hurt FX models.

In the next article or two, I will explore the 2011 performance of some other equities mean-reverting models that I used to trade. But what about your models? If you have some thoughts on what worked and what didn't in 2011, please share them with us in the comments section.
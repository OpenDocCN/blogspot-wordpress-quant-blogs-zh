<!--yml
category: 未分类
date: 2024-05-12 19:21:44
-->

# Quantitative Trading: How a mean-reversion strategy performed in August

> 来源：[http://epchan.blogspot.com/2007/10/how-mean-reversion-strategy-performed.html#0001-01-01](http://epchan.blogspot.com/2007/10/how-mean-reversion-strategy-performed.html#0001-01-01)

Prof. Andrew Lo and Mr. Amir Khandani at MIT recently wrote a paper on

["What Happened To The Quants In August 2007?"](http://web.mit.edu/alo/www/Papers/august07.pdf)

(Hat tip to my reader Mr. J. Rigg for the article). Most of their conclusions confirm what many observers already suspected: that the loss is likely due to the simultaneous forced liquidation of portfolios holding similar positions by various quantitative funds. What is noteworthy, however, is that they constructed a mean-reversion strategy and observed what happened to it during August. This strategy is very simple: buy the stocks with the worst previous 1-day returns, and short the ones with the best previous 1-day returns. Despite its utter simplicity, this strategy has had great performance since 1995, ignoring transaction costs. The Sharpe ratio was an astounding 53.87 in 1995, gradually decreasing to 4.47 in 2006\. However, the strategy also had a disastrous few days on August 7-9, suffering a cumulative (arithmetic) return of -6.85% in those 3 days. Then on August 10, it rebounded, like the rest of the quant funds, with a return of 5.92%, almost reversing all of its previous losses. For me, this experiment reveals three interesting points: 1) a simple price factor seems to capture most of the performance of the complex factor models run by the gigantic hedge funds; 2) even technical mean-reverting factors suffer losses, not just momentum (growth) factors based on fundamentals; and 3) if one wants to avoid disasters and enjoy spectacular returns, even a one-day holding period is too long. I haven't done the experiment myself yet, but I bet that if we were to liquidate the portfolio at market close each day, not only would we avoid the loss of -6.85% in those 3 days, but would probably end up with a positive return of a similar magnitude!
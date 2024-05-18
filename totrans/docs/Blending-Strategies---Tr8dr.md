<!--yml
category: 未分类
date: 2024-05-18 15:33:09
-->

# Blending Strategies | Tr8dr

> 来源：[https://tr8dr.wordpress.com/2010/05/28/blending-strategies/#0001-01-01](https://tr8dr.wordpress.com/2010/05/28/blending-strategies/#0001-01-01)

May 28, 2010 · 7:00 pm

In a number of my systematic strategies I evaluate hundreds or thousands of sub-strategies, using a blend of these to decide on the next period trade.

Assume we are trading from a portfolio of possible assets, going fractionally long or short on a sparse subset of possible assets in the portfolio.   For example I may be working with an equity portfolio of 2300 possible equities.   From period to period I may trade anywhere from 0-40 of these.

At time **t** we want to know the apriori “optimal” weights for time **t+1** for the 2300 assets.  Each of our sub-strategies predicts the best weights (trades) for time **t+1**.   We know the cumulative return, the average return, and risk adjusted return for each of these “paper” strategies.

**Approaches
Here were some approaches:**

1.  use the top N strategies by highest cumulative historical return, risk adjusted
    This works reasonably well if each strategy is trading with the same frequency.   However, with one of my strategies, some “paper” strategies trade 85% of the time and other maybe 5% of the time.   The cumulative returns of the less frequently traded will be much lower.
2.  use the top N strategies by average return, risk adjusted
    This equalizes the trading frequency problem however the low frequency strategies can dominate the selection if the low frequency have much higher returns.   The problem is that the aggregate strategy will rarely trade because the top N are dominated by low frequency traded strategies.
3.  use the top N **non-zero weights** strategies by average return, risk adjusted
    This avoids the dominating non-traded strategies above.   However there may be periods where the best trade is no trade at all.
4.  use the top N **non-zero weights** strategies with average return in the top X percent
    This fixes the above problem by just evaluating the top X percent at most in search of the top N trading strategies.

**A Complication**
One of my strategies has the following complication.  Many of the “paper” strategies are non-orthogonal in the sense that some of the strategies have overlapping stimuli and responses.   For example if 2 strategies are very similar, they may respond to the same events 80% of the time and have similar performance.   Including both of the strategies in the aggregate response will double count.

To avoid this have resorted to using a modified blending rule that discards strategies that are subsumed by higher performers in the selection.
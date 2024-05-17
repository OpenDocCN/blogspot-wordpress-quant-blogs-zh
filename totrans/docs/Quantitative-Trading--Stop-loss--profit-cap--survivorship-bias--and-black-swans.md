<!--yml
category: 未分类
date: 2024-05-12 19:02:23
-->

# Quantitative Trading: Stop loss, profit cap, survivorship bias, and black swans

> 来源：[http://epchan.blogspot.com/2011/09/stop-loss-profit-cap-survivorship-bias.html#0001-01-01](http://epchan.blogspot.com/2011/09/stop-loss-profit-cap-survivorship-bias.html#0001-01-01)

I have long espoused the view that we should not impose stop-losses on mean-reverting strategies, nor profit caps on momentum strategies. My view on the latter has not changed, but it has evolved on the former.

My original reason for opposing stop-losses on mean-reverting strategy is this. Say you believe your specific price series is mean-reverting, and say you have entered into a long position when the price is low. Now, however, the price gets much lower, and you are suffering a large unrealized loss. Well, based on your mean-reverting belief, you should buy more instead of liquidating! Indeed, if you backtest the effect of stop-losses on mean-reverting strategies, you will almost inevitably find that they decrease the overall returns and even Sharpe ratios.

But what this simplistic view ignored is 1) survivorship bias, and 2) black swan events. (Hat tip: Ben, who prompted me to consider these two issues.)

1) We normally would only trade those price series with a mean-reverting strategy only if we see that the prices did eventually revert. No one would bother to trade those price series that used to mean-revert, but suddenly stopped doing so. But saying that stop-losses are harmful to mean-reverting strategies is ignoring the fact that some mean-reverting will stop working altogether and would not survive our strategies selection process.

2) Let's define black swan events as those that did not occur in your backtest period. For example, let's say you never had a loss of 20% in a single day. So if you backtest a stop-loss of 20%, it will have no effect whatsoever on your backtest performance. However, no one can say for sure that it won't occur in the future. So if you or your investors simply cannot tolerate a 20% loss, you should impose this as a stop-loss. (After all, your brokerage has already imposed a stop-loss of 100% on you whether you like it or not.)

We can in fact turn point 2) around when deciding what stop-loss to use: a stop-loss should be loose enough so that it should have no effect on the backtest performance, and of course tight enough so that it will not result in the demise of your trading career.

There is also the issue of whether to use stop-loss on the intraday drawdown, or to use it on the multiple-day drawdown. I would argue that only intraday stop-loss is important to prevent a black-swan loss. In practice, when a strategy has a string of non-catastrophic losses occurring over multiple days, resulting in a large, unprecedented, drawdown, the trader will typically re-examine the strategy, taking into account this most recent performance and tweak the strategy so that it could theoretically be avoided. This is almost like a multi-day stop-loss strategy, as we stop an old strategy and start a new, modified, one. (Though the modified strategy might still recommend that you keep holding the current position!)

Now why am I still holding dear to the principle that one should not impose profit-caps on momentum strategies? Why, the possibility of black swan events again! But this time, any black swan can only result in unprecedented one-day

*gain*

instead of loss, since we should 

[always](http://epchan.blogspot.com/2009/06/my-interview-stop-loss-and-principle-of.html)

 have stop-losses on momentum strategies. We certainly don't want to impose a profit-cap to rule out this possibility!
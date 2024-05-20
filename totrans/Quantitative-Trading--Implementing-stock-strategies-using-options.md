<!--yml
category: 未分类
date: 2024-05-12 19:03:39
-->

# Quantitative Trading: Implementing stock strategies using options

> 来源：[http://epchan.blogspot.com/2010/09/implementing-stock-strategies-using.html#0001-01-01](http://epchan.blogspot.com/2010/09/implementing-stock-strategies-using.html#0001-01-01)

There are many stock trading strategies that are quite attractive in terms of Sharpe ratios, but not very attractive in terms of returns. (Pairs trading comes to mind. But in general, any market neutral strategy suffers from this problem.)  Certainly, one cannot feed a family with annualized returns in the single or low double digits, unless one already has millions of dollars of capital. One way to solve this dilemma is of course to join a proprietary trading group, where we would have access to perhaps x30 leverage. Another way is to implement a stock trading strategy using options instead, though there are a sizable number of issues to consider. (I recently brushed up on my options know-how by reading the popular "

[Options as a Strategic Investment](http://www.amazon.com/dp/0735201978?tag=quantitativet-20&camp=14573&creative=327641&linkCode=as1&creativeASIN=0735201978&adid=0Q0NBNQ5ETXJS894MZPP&)

".)

1.  Using options will allow you to increase your leverage beyond the Reg T x2 leverage (or even the day trading x4 leverage) only if you buy options only, but not selling them. For example, to implement a pairs trading strategy on 2 different stocks, you would have to buy call options on the long side, and *buy* put options on the short side (but not sell call options). Otherwise the margin requirement for selling calls is as onerous as shorting the underlying stock itself.
2.  The effective leverage is computed by multiplying the *delta* of the option by the underlying stock price divided by the option premium. If you buy an out-of-money (OTM) option, the delta will be small (smaller than 0.5), but the option premium is small also. Vice versa for an in-the-money (ITM) option. So you would have to find the optimal strike price so that the effective leverage is maximized. I personally choose to buy an at-the-money (ATM) call or slightly ITM call without actually computing the optimized strike, but perhaps you have reached a different conclusion?
3.  Naturally, the shorter the time-to-expiration, the cheaper the option and higher the effective leverage. Additionally, for ITM options, their deltas increase as we get closer to expiration, which also contributes to higher effective leverage. However, the time-to-expiration must of course be longer than the expected holding period of your position, otherwise you would incur the transaction cost of rolling over to the further-month options.
4.  The discussion of finding the right strike price based on its delta is moot if your brokerage's API does not provide you with delta for your automated trading system. In theory, Interactive Brokers's API provide deltas for whole options chains, and [quant2ib](http://exchangeapi.com/)'s MATLAB API will pass these on to your MATLAB exeuction program too. However, I have not been successful in retrieving deltas using quant2ib's API. If you have encountered a similar problem, and perhaps have found the reason/cure for this, please let me know. For now, I am reduced to assuming that all my near ATM calls for different stocks have the same delta, and I increase this common value from 0.5 to close to 1 as time passes.
5.  Options don't have MOO, LOO, MOC or LOC order types. If one uses market orders to buy at the open or close, one would incur significant transaction costs due to the much wider bid-ask spread compared to stocks. I try to use limit orders on options orders as much as possible.

If you have used options to implement stock trading strategies, and have experiences with these or other issues, please do share them here.

====

Reminder: my next

[pairs trading workshop](http://www.technicalanalyst.co.uk/training/pairs-trading.htm)

will take place in New York on October 26-27th.
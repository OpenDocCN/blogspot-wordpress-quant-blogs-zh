<!--yml
category: 未分类
date: 2024-05-12 18:59:20
-->

# Quantitative Trading: How Useful is Order Flow and VPIN?

> 来源：[http://epchan.blogspot.com/2013/10/how-useful-is-order-flow-and-vpin.html#0001-01-01](http://epchan.blogspot.com/2013/10/how-useful-is-order-flow-and-vpin.html#0001-01-01)

Can short-term price movement be predicted? (I am speaking of  seconds or minutes here.) This is a question not only relevant to high frequency traders, but to every long-term investor as well. Even if  one plans to buy and hold a stock for years,  nobody likes to suffer short-term negative P&L immediately after entry into position.

One short-term prediction method that has long found favor with academic researchers and traders alike is order flow. Order flow is just signed transaction volume: if a transaction of 100 shares is classified as a "buy", the order flow is +100; if it is classified as a "sell", the order flow is -100\. This might strike some as rather strange: every transaction has a buyer and seller, so what does it mean by a "buy" or a "sell"? Well, the "buyer" is defined as the one who is the "aggressor", i.e. one that is using a market order to buy at the ask price. (And vice versa for the seller, whom I will henceforth omit in this discussion.) The intuitive reason why a series of large "buy" market orders are predictive of short-term price increase is that if someone is so eager to go long, s/he is likely to know something about the market that others don't (either due to superior fundamental knowledge or technical model), so we better join her/him! Such superior traders are often called "informed traders", and their order flow is often called "toxic flow". Toxic, that is, to the uninformed market maker.

In theory, if one has a tick data feed, one can tell whether an execution is a "buy" or "sell" by comparing the trade price with the bid and ask price: if the trade price is equal to the ask, it is a "buy". This is called the "Quote Rule". But in practice, there is a hitch. If the bid and ask prices change quickly, a buy market order may end up buying at the bid price if the market has fortuitously moved lower since the order was sent. Besides, perhaps 1/3 of trading in the US equities markets take place in dark pools or via hidden orders, so the quotes are simply invisible and order flow non-computable. So this classification scheme is not foolproof. Therefore, a number of researchers (see "

[Flow Toxicity and Volatility in a High Frequency World](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1695596)

" by Easley, et. al.) proposed an alternative, "easier", method to compute order flow. Instead of checking the trade price of each tick, they just need the "open" and "close" trade prices of a bar, preferably a volume bar, and assign a fraction of the volume in that bar to "buy" or "sell" depending on whether the close price is higher or lower than the open price. (The assignment formula is based on the cumulative probability density of a Gaussian distribution, which incidentally models price changes of volume bars, but not time bars, pretty well.) The absolute difference between buy and sell volume expressed as a fraction of the total volume is called "VPIN" by the authors, or

*Volume-Synchronized Probability of Informed Trading*

. The higher VPIN is, the more likely we will experience short-term momentum due to informed trading.

Theory and intuition aside, how well does order flow work in practice as a short-term predictor in various markets? And how predictive is VPIN as compared to the old Quote Rule?  In my experience, while this indicator is predictive of price change, the change is often too small to overcome transaction costs including the bid-ask spread. And more disturbingly, in those markets where both Quote Rule and VPIN should work (e.g. futures markets), VPIN has so far underperformed Quote Rule, despite (?) it being patented and highly touted. I have informally polled other investment professionals on their experience, and the answer usually come back indifferent as well.

Do you have live experience with VPIN? Or more generally, do you find strategies built using volume bars superior to those using time bars? If so, please leave us your comments!

===

My online Quantitative Momentum Strategies workshop will be offered in December. Please visit 

[epchan.com/](http://epchan.com/my-workshops)[my-workshops ](http://epchan.com/my-workshops)

for registration details.
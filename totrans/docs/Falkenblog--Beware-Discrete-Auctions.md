<!--yml
category: 未分类
date: 2024-05-12 20:04:11
-->

# Falkenblog: Beware Discrete Auctions

> 来源：[http://falkenblog.blogspot.com/2013/07/beware-discrete-auctions.html#0001-01-01](http://falkenblog.blogspot.com/2013/07/beware-discrete-auctions.html#0001-01-01)

There's an interesting paper on High Frequency Trading (HFT) by

[Budish, Cramton, and Shim](http://faculty.chicagobooth.edu/eric.budish/research/HFT-FrequentBatchAuctions.pdf)

from the U of Chicago. They set up an interesting model, but then propose at the end that batching eliminates the HFT arms race, both because it reduces the value of tiny speed advantages and because it transforms competition on speed into competition on price. I think that solution is interesting, but would prefer the following

1.  add a 20ish millisecond randomizer to any incoming order (ie, a lag of anywhere from 0 to 20 milliseconds). Thus, if you know you are getting randomized, the marginal value of 1 millisecond is much smaller to the innovator, your place in the queue is noisy. 
2.  make a rule that those who receive fees (liquidity providers) must have such orders exist for at least 1 second. That would get rid of a lot of flash quotes that are trying to be too clever and simply clog the bandwidth.

In any case, we have several different exchanges, and so if there's a simple way to increase welfare, an exchange that adds any such rule would generate more traffic, and ultimately, imitation. Yet, that's how paying for liquidity provision (passive quotes) originated, as well as a bunch of other tactics. One thinks they are annoying features created in a smoke-filled room, but instead they were simply the result of giving market participants what they want. A retail trader can always opt-out by simply trading at the Volume-Weighted-Average Price (VWAP), because that gives you the average daily price that averages out all these shenanigans, so I really don't have any sympathy for those who are bothered by it: if you don't like the intraday game, don't play it!

But, I was intrigued by the idea of batch auctions, because I've heard people who think discrete auctions are better than continuous ones. I think they are not very good, and a simple example is an extreme of this, one can look at the performance of closing vs. opening prices. One is at the end of continuous trading, one where there's no trading. What happens?

Well, I looked at over 1000 stocks, from 2000 to today.  I excluded really small, low-priced stocks.   The Open-Open returns have slightly higher volatility (2% higher), but more importantly, there's a lot more 'mean reversion'.  The graph below shows the future returns(O-O or C-C), sorted each day into deciles by the immediate prior return (O-O or C-C, respectively), then averaged over all those days.

Basically, markets open at extremes that are quickly erased, allowing the market makers to pocket nice premiums for these temporary imbalances (you can't make money off this if you aren't a specialist).  Continuous trading takes such trades away from monopolists, and allows competition to work.  

These authors propose more frequent auctions to be sure, but the logic remains.
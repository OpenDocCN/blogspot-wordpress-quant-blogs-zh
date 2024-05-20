<!--yml
category: 未分类
date: 2024-05-12 19:03:53
-->

# Quantitative Trading: Pair trading technologies update

> 来源：[http://epchan.blogspot.com/2010/07/pair-trading-technologies-update.html#0001-01-01](http://epchan.blogspot.com/2010/07/pair-trading-technologies-update.html#0001-01-01)

Pair trading was invented two decades ago, but automating its implementation has only recently become fashionable with independent traders. But once the spotlight is on, innovations come fast and furious. Here are a number of recent developments that I find interesting:

1\. I mentioned

[previously](http://epchan.blogspot.com/2009/05/matlab-as-automated-execution-system.html)

the software called

[quant2ib](http://exchangeapi.com/ProductOverview.htm)

. It is an API which allows us to get market data and send orders from a Matlab program to Interactive Brokers (IB). I have used it extensively for our trading, and it is as reliable as IB's native API. Their latest version now includes functions for constructing a "combo" security. This combo security can be pairs of stocks, ETF's, futures, etc. (with the notable exception of currencies), and the API allows you to get market data as well as to submit orders on a combo. This is a huge improvement because you can now automatically trade a pair of securities as one unit by submitting

**limit**

orders on the combo. (Previously, you would have had to submit market order on at least one side of the pair, and this would have required your program to continuously monitor the market prices and send orders when appropriate. Or else you had to give up using the API and manually enter a "generic combo" limit order in IB's TWS.)

2\. Alphacet Discovery also has the ability to send limit orders on pairs, due to its

[partnership](http://alphacet.com/site/news/knight.shtml)

with Knight Trading. Besides, based on a demo that I have recently seen, they also now have great pairs portfolio and execution reporting functionality. (Full disclosure: I used to consult for them.)

3\. IB itself has released a "Scale Trader" algorithm that can be applied to combos (see 1\. above. Hat tip: Mohamed.) I can't explain this better than their press release: "... ScaleTrader algorithm allows clients to create conditions under which a long position in one stock is built while simultaneously creating an offsetting short position in the other. The ScaleTrader is named because investors can '

scale

-in' to market weakness by setting

orders

to buy as the market moves lower. Similarly, sell

orders

can be 'scaled' into when a market is rising. The ScaleTrader algorithm can be programmed to buy the spread and subsequently take profit by selling the spread if the difference reaches predetermined levels set by the user." In other words, it allows us to automatically implement the "

[parameterless trading](http://epchan.blogspot.com/2008/08/more-on-parameterless-trading-model.html)

" or the "

[averaging-in](http://epchan.blogspot.com/2010/01/does-averaging-in-work.html)

" strategy that I blogged about previously without any programming on our part!

Speaking of pair trading, I will be teaching my first New York

[workshop](http://www.technicalanalyst.co.uk/training/pairs-trading.htm)

in October.  (My editor inevitably picks touristy locations for these workshops. My London workshop takes place across the street from the Tower of London, my New York workshop is across from the new World Trade Center, and my Hong Kong workshop is in the "Golden Mile" shopping district of Tsim Sha Tsui.)
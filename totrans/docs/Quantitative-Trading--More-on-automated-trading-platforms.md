<!--yml
category: 未分类
date: 2024-05-12 19:02:28
-->

# Quantitative Trading: More on automated trading platforms

> 来源：[http://epchan.blogspot.com/2011/09/more-on-automated-trading-platforms.html#0001-01-01](http://epchan.blogspot.com/2011/09/more-on-automated-trading-platforms.html#0001-01-01)

The ideal software platform for automating backtesting and executing your algorithmic trading strategies depends mainly on your level of programming expertise and your budget. If you are a competent programmer in, say, Java or C#, there is nothing to prevent you from utilizing the API offered (usually for free) by many brokerages to automate execution. And of course, it is also easy for you to write a separate backtesting program utilizing historical data. However, even for programmer-traders, there are a couple of inconveniences in developing these programs from scratch:

A) Every time we change brokerages, we have to re-write parts of the low-level functions that utilize the brokerage's API;

B) The automated trading program cannot be used to backtest unless a simulator is built to feed the historical data into the program as if they were live. To reduce bugs, it is better to have the same code that both backtests and trades live.

This is where a number of open-source algorithmic trading development platforms come in. These platforms all assume that the user is a Java programmer. But they eliminate the hassles A) and B) above as they serve as the layer that shield you from the details of the brokerage's API, and let you go from backtesting to live trading mode with a figurative turn of a key. I have taken a tour of one such platforms

[Marketcetera](http://www.marketcetera.com/)

, and will highlight some features here:

1) It has a trading GUI with features similar to that of IB's TWS. This will be useful if your own brokerage's GUI is dysfunctional.

2) Complex Event Processing (CEP) is available as a module. CEP is essentially a way for you to easily specify what kind of market/pricing events should trigger a trading action. For e.g., "BUY if ask price is below 20-min moving average." Of course, you could have written this trading rule in a callback function, but to retrieve the 20-min MA on-demand could be quite messy. CEP solves that data retrieval problem for you by storing only those data that is needed by your registered trading rules.

3) It can use either FIX or a brokerage's API for connection. Available brokerage connectors include Interactive Brokers and Lime Brokerage.

4) It offers a news feed, which can be used by your trading algorithms to trigger trading actions if you use Java's string processing utilities to parse the stories properly.

5) The monthly cost ranges from $3,500 - $4,500.

If Marketcera is beyond your budget, you can check out

[AlgoTrader](http://code.google.com/p/algo-trader/)

. It has advantages 1)-3) but not 4) listed above, and is completely free. I invite readers who have tried these or other similar automated trading platforms to comment their user experience here.

P.S. For those of us who use Matlab to automate our executions, a reader pointed out there is a new product

[MATTICK](http://www.agoratron.com/our_products.html)

 that allows you to send order via the FIX protocol which should let us trade with a great variety of brokerages.
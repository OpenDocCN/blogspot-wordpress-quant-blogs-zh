<!--yml
category: 未分类
date: 2024-05-12 23:37:18
-->

# Front-Run The Delta: Index Arbitrage for the Do It Yourselfer

> 来源：[https://frontrunthedelta.blogspot.com/2011/06/index-arbitrage-for-do-it-yourselfer.html#0001-01-01](https://frontrunthedelta.blogspot.com/2011/06/index-arbitrage-for-do-it-yourselfer.html#0001-01-01)

This is the process used to construct a pseudo-

[Index Arbitrage](http://en.wikipedia.org/wiki/Index_arbitrage)

(similar to

[Delta One](http://www.efinancialnews.com/story/2011-06-10/delta-one-nomura)

) model of the

[SPDR Dow Jones Industrial ETF](https://www.spdrs.com/product/fund.seam?ticker=dia)

versus one of the front month ECBOT-listed

[E-Mini Dow Jones Industrial](http://www.cmegroup.com/trading/equity-index/us-index/e-mini-dow_contract_specifications.html)

futures contracts.  Our software is proprietary and was developed from scratch (not by me).  We are currently using

[IB's TWS](http://www.interactivebrokers.com/ibg/main.php)

as our medium to the markets.  It is my chemistry set.

**Constructing the Spread.**

Step 1: Define your bases.  Name your series.  In this case we name the file "DIA_YM".  The "t13,t14" corresponds to two of the variables on the left with open connections.  t01 through t12 are other securities currently being referenced by the software.

Step 2: Input your "proprietary" algorithm(s) of choice. As shown, currently blurred in boxes e01 through e06 (sorry, can't give it all away).

Step 3: Hit the LiveTrack(c)!

Step 4: Wait a few minutes and take a sample of the data.  This is very high-frequency, synchronized trade-and-quote data for the DIA/YM pair.  Synchronized (discussed 

[here](http://rogerenright.blogspot.com/2011/06/triangular-arbitrage-using-usdhkd.html)

) meaning when any predefined variable (bid, bid size, etc.) changes, a snapshot of the entire set is taken, time-stamped down to the millisecond

[,](http://en.wikipedia.org/wiki/Serial_comma)

and logged.

Step 5: Finally, check the result.  159 variable changes during 2 minutes and 13 seconds of sleepy after market trading.
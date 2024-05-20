<!--yml
category: 未分类
date: 2024-05-12 23:30:44
-->

# Front-Run The Delta: Recording TAQ Data via Interactive Broker's API & Teaser of Ericsson Arbitrage Study

> 来源：[https://frontrunthedelta.blogspot.com/2012/01/recording-taq-data-via-interactive.html#0001-01-01](https://frontrunthedelta.blogspot.com/2012/01/recording-taq-data-via-interactive.html#0001-01-01)

On October 28, reader "RKB" 

[asked](http://frontrunthedelta.blogspot.com/2011/09/request-arb.html#comments)

how I have been able to pull my data into Excel.  First, I would like to apologize to RKB for taking

*forever*

to answer his question. 

I have a program developed by a friend of mine, written in Java, that allows me to record time and sales for individual and groups of securities.  The program then dumps this data into a CSV file that I open with Excel.  All the manipulations in Excel I handle after the the price data has been cleaned and formatted into my formulas.

The software we developed is on the left with an

[IB Trader Workstation](http://www.interactivebrokers.com/en/p.php?f=tws&ib_entity=llc)

window open on the right showing some of the currencies available through

[IB's IDEAL PRO](http://www.interactivebrokers.com/en/trading/exchanges.php?exch=ibfxpro)

.  As you can see I have several open connections to a variety of currencies and several NYMEX natural gas futures contracts.

The program records bid, ask, bid size, ask size, last trade, last size, high, low, and close for equities, options, futures, future options, currencies, and combinations.  I cannot emphasize enough the importance of synchronized group recordings.  The weakness of using minute or even second by second quotes for arbitrage strudies is the nature of high-frequency arbitrage trading today makes these quotes obsolete.  You can record 2 seconds worth of data that consists of 100+ quote changes.

The last trade is never what's important.  The most important aspects of multiple-leg structures is the live bid, ask, and depth of market.  Liquidity risk has killed too many titans.

Here is the raw data for a study on

[triangular arbitrage](http://frontrunthedelta.blogspot.com/search/label/triangular%20arbitrage)

. For those interested, this software is

[for sale](mailto:jwilliams@murphywilliams.com)

.

It should be noted that IB is not the perfect platform to operate in today's market.  They are limited to pricing updates at a rate of 100ms when many of today's trades occur in the 10-20ms range.  This obstacle has limited my ability to study certain HFT strategies at higher granularities than I can record.

And a teaser for an upcoming post on

[ADR arbitrage](http://frontrunthedelta.blogspot.com/search/label/adr%20arbitrage)

across Ericsson shares...
<!--yml
category: 未分类
date: 2024-05-12 18:57:04
-->

# Quantitative Trading: Commitments of Traders (COT) strategy on soybean futures

> 来源：[http://epchan.blogspot.com/2015/02/commitments-of-traders-cot-strategy-on.html#0001-01-01](http://epchan.blogspot.com/2015/02/commitments-of-traders-cot-strategy-on.html#0001-01-01)

In our drive to extract alphas from a variety of non-price data, we came across this old-fashioned source: Commitments of Traders (COT) on futures. This indicator is well-known to futures traders since 1923 (see www.cmegroup.com/education/files/COT_FBD_Update_2012-4-26.pdf), but there are often persistent patterns (risk factors?) in the markets that refuse to be arbitraged away. It is worth another look, especially since the data has become richer over the years.

First, some facts about COT:

1) CFTC collects the reports of the number of long and short futures and options contracts ("open interest") held by different types of firms by Tuesdays, and reports them every Friday by 4:30 CT.

2) Options positions are added to COT as if they were futures but adjusted by their deltas.

3) COT are then broken down into contracts held by different types of firms. The most familiar types are "Commercial" (e.g. an ethanol plant) and "Non-Commercial" (i.e. speculators).

4) Other types are "Spreaders" who hold calendar spreads, "Index traders", "Money Managers", etc. There are 9 mutually exclusive types in total.

Since we only have historical COT data from csidata.com, and they do not collect data on all these types, we have to restrict our present analysis only to Commercial and Non-Commercial. Also, beware that csidata tags a COT report by its Tuesday data collection date. As noted above, that information is unactionable until the following Sunday evening when the market re-opens.

A simple strategy would be to compute the ratio of long vs short COT for Non-Commercial traders. We buy the front contract when this ratio is equal to or greater than 3, exiting when the ratio drops to or below 1\. We short the front contract when this ratio is equal to or less than 1/3, exiting when the ratio rises to or above 1\. Hence this is a momentum strategy: we trade in the same direction as the speculators did. As most profitable futures traders are momentum traders, it would not be surprising this strategy could be profitable.

Over the period from 1999 to 2014, applying this strategy on CME soybean futures returns about 9% per annum, though its best period seems to be behind us already. I have plotted the cumulative returns below (click to enlarge).

I have applied this strategy to a few other agricultural commodities, but it doesn't seem to work on them. It is therefore quite possible that the positive result on soybeans is a fluke. Also, it is very unsatisfactory that we do not have data on the Money Managers (which include the all important CPOs and CTAs), since they would likely to be an important source of alpha. Of course, we can go directly to the cftc.gov,

[download](http://www.cftc.gov/MarketReports/CommitmentsofTraders/HistoricalCompressed/index.htm)

all the historical reports in .xls format, and compile the data ourselves. But that is a project for another day.

===

**My Upcoming  Talks and Workshops**

5/13-14: "Mean Reversion Strategies", "AI techniques in Trading" and "Portfolio Optimization" at [Q-Trade Bootcamp 2015](http://qtradebootcamp.com/), Milan, Italy. 

===

**Managed Account Program Update**

===

Follow me on Twitter: @chanep
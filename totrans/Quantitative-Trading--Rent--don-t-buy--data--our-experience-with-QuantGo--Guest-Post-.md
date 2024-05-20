<!--yml
category: 未分类
date: 2024-05-12 18:57:19
-->

# Quantitative Trading: Rent, don’t buy, data: our experience with QuantGo (Guest Post)

> 来源：[http://epchan.blogspot.com/2014/11/rent-dont-buy-data-our-experience-with.html#0001-01-01](http://epchan.blogspot.com/2014/11/rent-dont-buy-data-our-experience-with.html#0001-01-01)

*By Roger Hunter*

I am a quant researcher and developer for QTS Partners, a commodity pool Ernie (author of this blog) founded in 2011\. I help Ernie develop and implement several strategies in the pool and various separate accounts.  I wrote this article to give insights into a very important part of our strategy development process: the selection of data sources.

Our main research focus is on strategies that monitor execution in milliseconds and that hold for seconds through several days. For example, a strategy that trades more than one currency pair simultaneously must ensure that several executions take place at the right price and within a very short time. Backtesting requires high quality historical intraday quote and trade, preferably tick data for testing.  Our initial focus was futures and after looking at various vendors for the tick data quality and quantity we needed, we chose Nanex data which is aggregated at 25ms. This means, for example, that aggressor flags are not available. We purchased several years of futures data and set to work.

Earlier this year we needed to update our data and discovered that Nanex prices had increased significantly. We also needed quotes and trades, and data for more asset classes including US equities and options.

We looked at TickData.com which has good data but is very expensive and you pay up-front per symbol.  There are other services like Barchartondemand.com and XIgnite.com where you pay based on your monthly usage (number of data requests made) which is a model we do not like.  We ended up choosing

[QuantGo.com](http://tinyurl.com/oxv4d6k)

, where you have unlimited access to years of global tick or bar data for a fixed monthly subscription fee per data service.

On QuantGo, you get computer instances in your own secure and private cloud built on Amazon AWS with on-demand access to a wide range of global intraday tick or bar data from multiple data vendors.  Since you own and manage the computer instances you can choose any operating system, install any software, access the internet or import your own data.  With QuantGo the original vendor data must remain in the cloud but you can download your results, this allows QuantGo to rent access to years of data at affordable monthly prices.

All of the data we have used so far is from AlgoSeek (one of QuantGo’s data vendors). This data is survivorship bias-free and is exactly as provided by the exchanges at the time. Futures quotes and trades download very quickly on the system. I am testing options strategies, which is challenging due to the size of the data. The data is downloaded in highly compressed form which is then expanded (by QuantGo) to a somewhat verbose text form.  Before the price split, a day of option quotes and trades for AAPL was typically 100GB in this form. Here is a data sample from the full Options (OPRA) data:

Timestamp, EventType, Ticker, OptionDetail, Price, Quantity, Exchange, Conditions

08:30:02.493, NO_QUOTE BID NB, LLEN, PUT at 7.0000 on 2013-12-21, 0.0000, 0, BATS, F

08:30:02.493, NO_QUOTE ASK, LLEN, CALL at 7.0000 on 2013-12-21, 0.0000, 0, BATS, F

09:30:00.500, ROTATION ASK, LLEN, PUT at 2.0000 on 2013-07-20, 0.2500, 15, ARCA, R

09:30:00.500, ROTATION BID, LLEN, PUT at 2.0000 on 2013-07-20, 0.0000, 0, ARCA, R

09:30:00.507, FIRM_QUOTE ASK NB, LLEN, PUT at 5.0000 on 2013-08-17, 5.0000, 7, BATS, A

09:30:00.508, FIRM_QUOTE BID NB, LLEN, PUT at 6.0000 on 2013-08-17, 0.2000, 7, BATS, A

These I convert to a more compact format, and filter out lines we don't need (e.g. NO_QUOTE, non-firm, etc.)

The quality of the AlgoSeek data seems to be high. One test I have performed is to record live data and compare it with AlgoSeek. This is possible because the AlgoSeek historical data is now updated daily, and is one day behind for all except options, which varies from two days to five (they are striving for two, but the process involves uploading all options data to special servers --- a significant task). Another test is done using OptionNET Explorer (ONE). ONE data is at 5-minute intervals and the software displays midpoints only. However, by executing historical trades, you can see the bid and ask values for options at these 5-minute boundaries. I have checked 20 of these against the AlgoSeek data and found exact agreement in every case. In any event, you are free to contact the data vendors directly to learn more about their products. The final test of data quality (and of our market model) is the comparison of live trading results (at one contract/spread level) with backtests over the same period.

The data offerings have recently expanded dramatically with more data partners and now include historical data from (QuantGo claims) "every exchange in the world". I haven't verified this, but the addition of elementized, tagged and scored news from Acquire Media, for example, will allow us to backtest strategies of the type discussed in Ernie's latest book.

So far, we like the system. For us, the positives are:

1\. Affordable Prices.  The reason that the price has been kept relatively low is that original vendor data must be kept and used in the QuantGo cloud. For example, to access years of US data we have been paying

Five years of US Equities Trades and Quotes (“TAQ”) is $250 per month

Five years of US Equities 5 minute Bars $75 per month

Three Years of US Options 1 minute bars $100 per month.

Three Year of CME, CBOT, NYMEX Futures Trades and Quotes $250 per month

2\.  Free Sample Data.  Each data service has free demo data which is actual real historical data where I can select data from the demo date range.  This allowed me to view and work with the data before subscribing.

3\. One API.  I have one API to access different data vendors.  QuantGo gives me a java GUI, python CLI and various libraries (R, Matlab, Java).

4\. On-Demand.  The ability to select the data we want "on demand" via a subscription from a website console at any time. You can select data for any symbol and for just a day or for several years.

5\. Platform not proprietary.  We can use any operating system or software with the data as it is being downloaded to virtual computers we fully control and manage.

Because all this is done in the cloud, we have to pay for our cloud computer usage as well.  While cloud usage is continuing to drop rapidly in price it is still a variable cost and it needs to monitored.  QuantGo does provide close to real-time billing estimates and alarms you can preset at dollar values.

I was at first skeptical of the restriction of not being able to download the data vendor’s tick or bar data, but so far this hasn't been an issue as in practice we only need the results and our derived data sets. I'm told that if you want to buy the data for your own computers, you can negotiate directly with the individual data vendor and will get a discount if you have been using it for a while on QuantGo.

As we use the windows operating system we access our cloud computers with Remote Desktop and there have been some latency issues, but these are tolerable. On the other hand, it is a big advantage to be able to start with a relatively small virtual machine for initial coding and debugging, then "dial up" a much larger machine (or group of machines) when you want to run many compute and data intensive backtests. While

[QuantGo](http://tinyurl.com/oxv4d6k)

is recently launched and is not perfect, it does open up the world of the highest institutional quality data to those of us who do not have the data budget of a Renaissance Technologies or D.E. Shaw.

=== **Industry Update**

(No endorsement of companies or products is implied by our mention.)

*   A new site for jobs in finance was recently launched: [www.financejobs.co](http://www.financejobs.co/).
*   A new software package Geode by Georgica Software can backtest tick data, and comes with a fairly rudimentary fill simulator.
*   [Quantopian.com](http://quantopian.com/) now incorporates a new IPython based research environment that allows interactive data analysis using minute level pricing data in Python.

===

**Workshops Update**

My next online [Quantitative Momentum Strategies](http://www.epchan.com/workshops/) workshop will be held on December 2-4\. Any reader interested in futures trading  in general would benefit from this course.

===

**Managed Account Program Update**

Our FX Managed Account program had an unusually profitable month in

[October](http://www.epchan.com/accounts/)

.

===

Follow me on Twitter: @chanep
<!--yml
category: 未分类
date: 2024-05-12 18:35:21
-->

# Rotation Concepts | CSSA

> 来源：[https://cssanalytics.wordpress.com/2010/02/23/rotation-concepts/#0001-01-01](https://cssanalytics.wordpress.com/2010/02/23/rotation-concepts/#0001-01-01)

For all examples in this post I am using the Rotation application in ETF Rewind: [http://marketrewind.blogspot.com/2010/02/etf-rewind-announcing-customizable.html](http://marketrewind.blogspot.com/2010/02/etf-rewind-announcing-customizable.html)

Rotational or relative strength models are a simple means of buying the stocks or ETFs that either have the strongest trend or are rising the fastest. The methods for creating effective relative strength models are beyond the scope of this article, but suffice to say there are a wide variety of different types. What makes a good relative strength/rotational model is the ability to deliver: 1) a high return/risk-adjusted return 2) moderate turnover 3) capability of adapting to bear markets 4) speed of adaptation–this is directly related to drawdown risk. The ETF Rewind Rotation tool has all of these features–while a simple 52 week ROC momentum strategy clearly does not. Classic RS strategies all use 52-week ROC in some capacity, and the highest-ranked stocks have massively underperformed the lowest-ranked stocks in the last couple years. If you have done any due diligence or research–this should not have come as a surprise, however it is a highly durable abeit long-term strategy. A 52-week ROC strategy will have its periods of over/underperformance, but will persist over long periods of time due to its robustness—even more so in my opinion than say timing with a 200-day moving average.

All of that aside, there is a lot more required to develop a good strategy than just a good algorithm. Rotational strategies are relative, and they depend on the universe of stocks/ETFs that are chosen. This is actually the most critical step to building a good model. Other questions pertain to how many assets (stocks/ETFs) you will select and how often you will rotate. What we are looking for in this case is to rotate across assets that have: **1) low inherent correlation**–ideally you will have different asset classes or sectors. A low correlation is the only thing that allows you to truly have a free lunch because it reduces risk substantially without hurting returns as much as more correlated strategies. Futhermore, even if you choose only one asset, a low correlation will permit near sequentially independent opportunities: this means that one asset can be moving higher while the rest are falling or consolidating- potentially allowing you to surf new waves all the time. This technique is impossible to accomplish with an inherently correlated asset universe such as 5 stocks within the same sector. Another important feature of your selection criterion for rotation models are assets with **2) inherently good potential reward/volatility** which is often found by using an index ETF, or commmodity or large capitalization stocks—anything else requires tremendous diversification to be effective. The issue with small stocks for example is earnings or news risk which can cause a stock to tank 40-50% in one day, or rise several hundred percent. Their high idiosyncratic risk makes them a very risky proposition—but even more importantly they have very high trend failure rates: small stocks do not tend to hold their trends as long as large stocks (in turn these are inferior to sectors, which are inferior to indexes, and asset classes etc). This increases turnover in rotational models, and also makes it difficult for the algorithm chosen to determine when to switch.

*Lets look at the first example. All tests use the REWIND model and backtests are 3-years in duration from March 2007 to present. The method is LONG ONLY*

Lets use the three major index ETFs to start: SPY, IWM, QQQQ and choose the top #1\. Here are the results:

Hypothetical
Top # Performance
1 Model SPY
3-Yr. Gross +1.8% -14.5%
C.A.G.R. +0.6% -5.1%
Sharpe 0.02 0.19
Maximum +13.3% +13.3%
Minimum -16.3% -19.8%
Average +0.1% -0.0%

This is certainly very reasonable performance–better than most relative strength algorithms that were longer-term over this brutal bear market. However in an absolute sense, the returns are still quite low–reflecting the fact that there was nowhere to rotate to when the market went down. The indexes are too highly correlated to use on a standalone basis. So what about “international diversification” ie the overblown concept most often touted by ill-informed or complacent financial advisors? Lets take a look–here I will add EEM- the emerging markets ETF which covers the BRIC countries and many more and EFA- which covers the MSCI EAFE index (Europe, Asia and the Far East). Although there is some overlap, these two are the biggies that pretty much cover the rest of the world. Again in this test we will rotate to the top index.

Hypothetical
Top # Performance
1 Model SPY
3-Yr. Gross +9.0% -15.0%
C.A.G.R. +2.9% -5.3%
Sharpe 0.09 0.17
Maximum +13.3% +16.5%
Minimum -16.3% -16.3%
Average +0.1% -0.0%

A modest return improvement, but clearly not enough diversification to make a material difference. After all the correlations between the indexes are quite high, and especially so in bear markets (note that in bull markets this differential would be much larger). Lets now add some real diversifiers– bonds and short-term bonds/cash. For bonds we will use AGG- Lehman Aggregate Bond Index , and for a cash proxy we will use SHY which is the 1-3 year Barclays treasury bond index. Lets look at the results:

Hypothetical
Top # Performance
1 Model SPY
3-Yr. Gross +44.7% -15.0%
C.A.G.R. +13.1% -5.3%
Sharpe 0.61 0.17
Maximum +8.6% +16.5%
Minimum -11.2% -16.3%
Average +0.3% -0.0%

OK so much better results in this run. A CAGR of 13% in this bear market was nothing to sneeze at, especially with a Sharpe Ratio of .61\. As you can clearly see, the ability to rotate to uncorrelated assets was a major help, and sort of a market timing tool. Any rotation model MUST have bonds or cash—and preferably a cash proxy like SHY since it has much less downside. Forget about all of the silly anecdotes about raising cash in bear markets etc–that is far too vague. Using the REWIND rotation model its quite simple–if cash is number 1 its time to get the #$&% out of the market. I can imagine sophisticated readers may have been rolling their eyes at the talk of diversification etc, but truthfully in reference to relative strength many MBAs,CFAs and PhD’s fail to put cash/bonds in their rotational models (including yours truly in earlier iterations many moons ago).

In the next post we will improve upon this substantially by expanding upon the same concepts. Furthermore, I will show you some cool tricks to employ to make things a lot better.
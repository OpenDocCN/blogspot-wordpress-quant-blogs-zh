<!--yml
category: 未分类
date: 2024-05-12 18:54:04
-->

# Quantitative Trading: Welcome to Our Feature Zoo with 600+ features!

> 来源：[http://epchan.blogspot.com/2021/09/welcome-to-our-feature-zoo-with-600.html#0001-01-01](http://epchan.blogspot.com/2021/09/welcome-to-our-feature-zoo-with-600.html#0001-01-01)

 This has been a summer of feature engineering for PredictNow.ai. First, we launched the US stock [cross-sectional](https://www.predictnow.ai/blog/introducing-pre-engineered-stock-fundamental-features-at-predictnow-ai/) features and the [time-series](https://www.predictnow.ai/blog/metalabeling-and-the-duality-between-cross-sectional-and-time-series-factors/) market-wide features. Now we have launched the features based on options activities, ETFs, futures, and macroeconomic indicators. In total, we are now offering 616 ready-made features to our subscribers.

There is a lot to read here. If you would rather join our October 1, 12pm EST webinar where Ernie and I will discuss these factors / features and answer your questions, please sign up [here](https://py.predictnow.ai/register_workshop).

NOPE - [Net options pricing effect](https://www.scribd.com/document/487296659/Investigating-Delta-Gamma-Hedging-Impact-on-SPY-Returns-2007-2020) - is a normalized measure of the net delta imbalance between the put and call options of a traded instrument across its entire option chain, calculated at the market close for contracts of all maturities. This indicator was invented by Lily Francus (Twitter: @nope_its_lily) and is normalized with the total traded volume of the underlying instrument. The imbalance estimates the amount of delta hedging by market markers needed to keep their positions delta-neutral. This hedging causes price movement in the underlying, which NOPE should ideally capture. The data for this has been sourced from [Delta Neutral](http://www.deltaneutral.com/).and the instrument we applied it to was SPY ETF options. The SPX index options were’t used because the daily traded volume of the underlying SPX index “stock” was irrational. It was calculated as the traded volume of the constituents of the index.

Canary - is an indicator that acts similar to a  canary in a coal mine, which will raise an alarm when there’s an impending danger. This indicator comes from the dual momentum strategies of [Vigilant](https://seekingalpha.com/article/4087925-breadth-momentum-and-vigilant-asset-allocation) and [Defensive Asset allocation](https://indexswingtrader.blogspot.com/2018/07/announcing-defensive-asset-allocation.html). The canary value can be either 0,1 or 2\. This is a daily measure of which of the two bond or stock ETFs has a negative absolute momentum - 1) BND - Vanguard Total Bond Market ETF  2) VMO - Vanguard Emerging Markets Stock Index Fund ETF. The momentum is calculated using the 13612W method where we take a proportionally weighted average of percentage change in the bond/stock ETF returns in the last 1 month, 3 months, 6 months, and 1 year. In the paper, the values of “0”,”1” or “2” of the canary portfolio represent what percentage of the canary is bullish. This indicates  what proportion of the asset portfolio was allocated to global risky assets (equity, bond and commodity ETFs) and what proportion was allocated to cash. For example, a “2” would imply 100% cash or cash equivalents, while a “0” would imply 100% allocation to the global risky assets. Alternatively, a value of “1” would imply 50% allocation to global risky assets and 50% to cash. 

Carry - “[Carry](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2298565)”,  defined a carry feature as, “the return on a futures position when the price stays constant over the holding period”. (It is also called “roll yield” or “convenience yield”.) We calculate carry for 1) global equities - calculated as a ratio of expected dividend and daily close prices; 2) SPX futures - calculated from price of front month SPX futures contract and spot price of the index; and3) Currency -  calculated from the two nearest months futures data.

Macro factors - macro factors are derived from global macroeconomic data, from the US and 12 other major economies. These are sourced from either Factset or FRED. The factors being offered are:

1) US Market index adjusted by inflation, money supply - mainly calculated for the US - SP500 adjusted for CPI, PCE, M1 and M2 - tells us if the market index is “inflated” or bubbled up by increased money supply or increasing prices. All these features are daily percentage changes, to make them stationary. 

2) Principal components of continuous maturity bond data

Pricing factors can be extracted as the principal components of the cross-section of treasury yields i.e. these factors are linear combinations of the treasury yields. The first three PCs have been prime candidates in this regard as they generally explain over 99% of the variability in the term structure of bond yields and, due to their loadings, may be interpreted as the level, slope and curvature factor. More can be explored in the paper, [Equity tail risk in the treasury bond market](https://www.sipotra.it/wp-content/uploads/2021/01/Equity-tail-risk-in-the-treasury-bond-market.pdf).

3) Common sovereign ratios (calculated month-on-month and year-on-year)-

1.  Sovereign Debt normalised with GDP

2.  Foreign Exchange normalised with GDP, 

3.  Government spending normalised to GDP 

4.  Current account balance to normalised GDP

5.  Government Budget balance normalised by GDP

6.  Labour force as a percentage of population

4) Fixed income term premia - the risk or the term premium is the premium or compensation the bond holder gets to account for the possibility of short-term interest rates to deviate from the expected path. This is sourced from the FRED. The methodology for the term structure model used to calculate term premia is covered in the paper, [Three-Factor Nominal Term Structure Model](https://www.federalreserve.gov/data/three-factor-nominal-term-structure-model.htm). All the term premia features are daily percentage changes, to make them stationary. 

5) Features that are calculated as month-on-month and year-on-year percentage changes: 

1.  Current Account Balance - the percentage change in a country’s international transactions with other countries. 

2.  Exports - the percentage change in a country’s exports to other countries.

3.  Industrial production - the percentage change in a country’s output by industrial sector. 

4.  Imports - the percentage change in a country’s imports from other countries. 

5.  Money supply - the percentage change in a country’s M2 money supply. 

6.  Retail Sales Index- the percentage change in a country’s demand for durable and non-durable goods. 

7.  Employment -  the percentage change in a country’s employment numbers. 

8.  Housing Starts - the percentage change in a country’s new residential construction projects. 

9.  Trade balance - the percentage change in a country’s net sum of imports and exports. 

10.  Unemployment rate - the percentage change in a country’s percentage of labour that is jobless.

11.  Labour force - the percentage change in a country’s active labour force. 

12.  Foreign Exchange Reserves - the percentage change in a country’s forex reserves. 

13.  Consumer Price Index - the percentage change in a country’s CPI inflation measure.

14.  Wholesale Price Index - the percentage change in a country’s WPI inflation measure. 

6) Features that are calculated as quarter-on-quarter change:

1.  Government Spending - the percentage change in a country’s government spending.

2.  Fixed Investment - the percentage change in a country’s assets.

3.  Personal Consumption Expenditure - the percentage change in a country’s household expenditures.

4.  Government debt - the percentage change in a country’s government debt.

5.  Gross Domestic product - the percentage change in a country’s gross domestic product.

6.  Read Gross domestic product - GDP adjusted for inflation.

7.  GDP Price deflator -  the percentage change in a country’s price levels.

7) Seasonally adjusted features - calculated using additive seasonal decomposition to break the series into trend, seasonal and noise components. Only the trend is extracted to get a seasonally adjusted signal. After seasonal adjustment, we calculate the month-on-month and year-on-year change.

a) Seasonally adjusted Employment 

b) Seasonally adjusted  Retail Sales Index 

c) Seasonally adjusted Housing Starts 

8) Total Credit to the non-financial sector- 

The measure of the credit given to non-financial sectors in selected developed economies. This is a leading indicator and can inform us about movement in indicators like Gross domestic product in the future. We calculate the quarter-on-quarter change for these features.

9) Treasury Interest rate spreads - various combinations of spreads between sovereign yields of various maturities. These produce the slopes of the yield curves. Read more about the difference between term spread and term premium [here](https://russellinvestments.com/nz/blog/to-fear-or-not-to-fear-the-yield-curve).

10) Retail Inventory to Sales ratio - The percentage of inventory for durable and non-durable goods is sold. This can forecast changes in gross domestic product. We calculate the month-on-month change for these features.

11) Feds Fund rate - daily percentage change in the interbank overnight rate at which excess reserves based on bank requirements are lent or borrowed. The FOMC makes its decisions about rate adjustments based on key economic indicators that may show signs of inflation, recession, or other issues that can affect sustainable economic growth.

Orderflow

The underlying reason for the price movement for an asset is the imbalance of buyers and sellers. An onslaught of market sell orders portends a decrease in price and vice versa..

Order flow is the signed transaction volume aggregated over a period of time and over many transactions in that period to create a more robust measure. It’s also positively correlated with the price movement. This feature is calculated using tick data from Algoseek with aggressor tags (which flag the trade as a buy or sell market order). The data is time-stamped at milliseconds. We aggregate the tick-based order flow to form order flow per minute. 

An example: 

Order flow feature with time stamp 10:01 am will consider trades from 10:00:00 am 10:00:59 am

Time  Trade Size  Aggressor Tag

10:00:01 am  1  B

10:00:03 am  4  S

10:00:09 am  2  B

10:00:19 am  1  S

10:00:37 am  5  S

10:00:59 am  2  S

The order flow would be 1-4+2-1-5-5=-9

This would be reflect in our feature as Time:10:01 , Order flow :-9

Conclusion

With the 616 features PredictNow.ai  has developed for  our subscribers, applying machine learning to risk management and portfolio optimization is easier than ever , especially given our built-in financial machine learning API. Our [features importance ranking and selection function](https://www.predictnow.ai/blog/the-amazing-efficacy-of-cluster-based-feature-selection/) can indicate which of our  features are most important to predict a user’s portfolio or strategy’s return, so there’s no need to spend hours deciding on which features to include. . Ideally, a user  will also merge them with their own proprietary features to improve predictive accuracy. If you have any questions or would like to learn more about these features, download our detailed user manual [here](https://py.predictnow.ai/get_manual/), or book a live demo and chat with one of our consultants [here](https://www.predictnow.ai/contact/).
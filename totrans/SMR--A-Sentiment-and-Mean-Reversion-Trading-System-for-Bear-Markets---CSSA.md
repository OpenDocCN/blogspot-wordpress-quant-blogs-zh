<!--yml
category: 未分类
date: 2024-05-12 18:50:50
-->

# SMR- A Sentiment and Mean-Reversion Trading System for Bear Markets | CSSA

> 来源：[https://cssanalytics.wordpress.com/2009/08/18/smr-a-sentiment-and-mean-reversion-trading-system-for-bear-markets/#0001-01-01](https://cssanalytics.wordpress.com/2009/08/18/smr-a-sentiment-and-mean-reversion-trading-system-for-bear-markets/#0001-01-01)

Going long during bear markets can be a very scary proposition. Extreme RSI 2 or DV2 readings give us little consolation when peering over at the abyss. I wanted to design a system that incorporated a variety of factors to maximize the probability of success, and minimize the probability of an extreme loss. I also wanted a system that would be in the market for as little time as possible. I call the system “SMR” because it combines  sentiment indicators along with  mean-reversion indicators. I define bear markets in this case as the SPY being below its 252-day average. Here are the system inputs:

Mean-Reversion Indicators

1) unbounded DV2

2) daily follow through

3) DVS (the stretch indicator)

Sentiment Indicators

1) the VIX- volatility index

2) Gold and Silver — via the Central Fund of Canada (CEF) a favorite of true gold bugs

**SMR** System Rules:

It is a bear market: SPY is < 252-day average of closing prices

1) The DV2 unbounded is less than zero

2) The market is  lower than yesterday’s close

3) The DVS is less than the 50th percentile

4) The SPY outperformed CEF since yesterday’s close

5) The VIX is higher than yesterday’s close

If all of these rules are all satisfied buy the SPY on close, sell when the criteria are no longer met (usually trades last 1 day). Here are the results for the last 2 years:

| **SMR System 23/08/2007- Present** |   |
|   |
|   | Avg Gain | % Correct | Max Loss | Max Gain | # Trades |   |
| Buy Signals | 1.7% | 80.2% | -4.40% | 14.50% | 25 |   |
|   |   |   |   |   |   |   |
| **SMR System 23/08/2007- Present Performance Summary** |   |
|   |
|   | CAGR | StDev | Sharpe | R-Square | DVR (Sharpe x R-square) |   |
| Buy Signals | 22.0% | 13.4% | 1.59 | 88% | **1.40** |   |

System performance is very good with an annual compound return of 22%, and the equity curve is very smooth with an R-square of 88%.  The average hold is less than 1.1 days, and the maximum loss is only -4.4%.  There were only two trades that triggered two days in a row, and they were both winners.
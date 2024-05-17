<!--yml
category: 未分类
date: 2024-05-12 18:32:09
-->

# A Simple Adaptive Change to Daily Follow-Through to Capture Cycle Changes | CSSA

> 来源：[https://cssanalytics.wordpress.com/2010/04/07/a-simple-adaptive-change-to-daily-follow-through-to-capture-cycle-changes/#0001-01-01](https://cssanalytics.wordpress.com/2010/04/07/a-simple-adaptive-change-to-daily-follow-through-to-capture-cycle-changes/#0001-01-01)

| **Adaptive Cycle Shift Versus Static Reverse Follow-Through Variants** |
|   |   |   |   |
| S&P500 Index Last 2500 bars |   |   |   |
|   | Adaptive  | Standard Reverse | 2-day Reverse |
|   | Cycle Shift | Daily Follow Through |  Follow Through |
| CAGR | **32.0%** | 27.4% | 22.4% |
| DVR | **0.85** | 0.73 | 0.56 |
| Simple Sharpe | **1.46** | 1.26 | 1.02 |
|   |   |   |   |
| **2010 Performance** | **8.50%** | -1.09% | 9.25% |
| (Total Return) |   |   |   |

I cannot pretend to be a pioneer in cycle research, but I do know that there is a high degree of conceptual appeal and actual validity substantiated by my own results to this approach. The new set of adaptive indicators are forthcoming on Monday for the release of our **DV Indicators Excel Plug-in.** This power tool is for serious researchers and traders or just for people who don’t have standard platforms like Tradestation or Amibroker. The plug-in will feature all the old and new DV Indicators as well as this whole new class of self-adapting indicators and “cycle-shifters.” This “Level 1” adaptation is the next generation of indicators and the plug-in will be the ideal delivery mechanism for Level 2 and 3.

Michael Stokes at MarketSci observed that mean-reversion has been taking it on the chin recently and investigated the possibility that short-term mean-reversion was waning:  [http://marketsci.wordpress.com/2010/04/06/the-death-of-short-term-mean-reversion/](http://marketsci.wordpress.com/2010/04/06/the-death-of-short-term-mean-reversion/)  His conclusion was that this is a temporary anomaly and that mean-reversion is here to stay– I completely agree on this point. However, since all of the DV oscillators have been doing very well lately, I decided that I might try to explain the strange divergence. [https://cssanalytics.wordpress.com/2010/03/29/iron-chef-battle-oscillator-rsi2-and-dv-spy/](https://cssanalytics.wordpress.com/2010/03/29/iron-chef-battle-oscillator-rsi2-and-dv-spy/)   ***In truth the reality is that the market has not really changed in mean-reversion character so much as it has shifted cycles–that is the length of time required to complete a mean-reversion type trade is increasing.*** (note that this is not as useful of a moderating factor in follow-through or trend type markets). This is a function of volatility decreasing, and is even more exacerbated by the fact that the momentum/trend is increasing at a higher than normal rate. For DV Oscillators, this is somewhat less of an issue since they re-scale to current market volatility by self-adjustment. However for static measures, it might be instructive to question whether a 1-day cycle that is typical of reverse daily follow-through and also highly correlated to binary RSI2 is simply too short for these market conditions? 

Ultimately, the long-term trend dictates such large scale shifts in volatility and momentum. But instead of focusing on being concerned with filtering long or short trades, the long-term trend can be used to filter for changes in the cycle length. In this case, one simple change makes a big difference. Below is the performance of regular reverse daily follow through (long on down days, short on up days) and the performance of 2-day reverse daily follow through (long if the two day performance is negative and short if positive) depending on the long-term trend as defined by the 50 day sma relative to the 200 day sma (aka the Golden Crossover). The test run below was on the S&P500 index (^GSPC) over the last 3000 bars which is more reliable for close to close strategies (pointed out by MarketSci).

|   |   |   |
| **Long-term Trend is DOWN (50sma<200sma)** |
|   |   |   |
| ***regular (one-day) reverse follow-through*** |
|   |   |   |
| cagr | 13.37% | below |
| avg daily | 0.06% |   |
| avg daily/vol | **5.02%** |   |
| dvr | **0.331273** |   |
| ssharpe | 0.747484 |   |
|   |   |   |
| ***two-day reverse follow-through*** |
|   |   |   |
| cagr | 7.46% | below |
| avg daily | 0.04% |   |
| avg daily/vol | **3.11%** |   |
| dvr | **0.067656** |   |
| ssharpe | 0.416696 |   |

| **Long-term Trend is UP (50sma>200sma)** |
|   |   |   |   |
| ***regular (one-day) reverse follow-through*** |
|   |   |   |   |
| cagr | 4.68% |   |   |
| avg daily | 0.02% |   |   |
| avg daily/vol | **2.73%** |   |   |
| dvr | **0.289371** |   |   |
| ssharpe | 0.375935 |   |   |
|   |   |   |   |
| ***two-day reverse follow-through*** |
|   |   |   |   |
| cagr | 6.77% |   |   |
| avg daily | 0.03% |   |   |
| avg daily/vol | **3.74%** |   |   |
| dvr | **0.404976** |   |   |
| ssharpe | 0.543899 |   |   |

As you can see when the long-term trend is DOWN, the standard reverse daily follow through approach is vastly superior in absolute and risk-adjusted returns to the two-day follow through strategy. However, when the long-term trend is UP, the two-day reverse follow-through strategy is superior in both respects. Note that most combinations of longer reverse-follow through lengths and/or indicators  have performed more consistently when the long-term trend is UP. The only logical explanation for this is that the cycle lengths increase as a function of lower volatility and more consistent momentum/trend. The solution is clearly to shift to longer cycles in this environment.
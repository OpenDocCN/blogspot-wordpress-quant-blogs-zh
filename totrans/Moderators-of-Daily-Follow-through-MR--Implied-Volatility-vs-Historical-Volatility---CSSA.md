<!--yml
category: 未分类
date: 2024-05-12 18:50:18
-->

# Moderators of Daily Follow-through MR: Implied Volatility vs Historical Volatility | CSSA

> 来源：[https://cssanalytics.wordpress.com/2009/08/25/moderators-of-daily-follow-through-mr-implied-volatility-vs-historical-volatility/#0001-01-01](https://cssanalytics.wordpress.com/2009/08/25/moderators-of-daily-follow-through-mr-implied-volatility-vs-historical-volatility/#0001-01-01)

Before getting into this topic I recommend some background reading as I will be delving quickly into results:

This recent article by Bill Luby inspired me to take a look at the linkage between implied and historical volatility with relevance to short-term trading.  It contains links to previous articles on the topic can be found on the blog site VIX and More: [http://vixandmore.blogspot.com/2009/08/gap-between-vix-and-realized-volatility.html](http://vixandmore.blogspot.com/2009/08/gap-between-vix-and-realized-volatility.html)

For another very good article with relevant background reading that helped further clarify my theories on the topic, Jared Woodward of Condor Options discusses how to create a trading system using historical vs implied volatility:  [http://www.condoroptions.com/index.php/volatility/historical-and-implied-volatility-crossovers/](http://www.condoroptions.com/index.php/volatility/historical-and-implied-volatility-crossovers/)

To summarize their results, when implied volatility (IV) is greater than historical volatility (HV) the market tends to outperform and vice versa. Note to readers: to avoid any confusion this post is not about “realized volatility” because i do not lag the values of the VIX to see how it forecasted historical volatility. All I have done is to subtract current 30-day  historical volatility from current implied volatility via the VIX  .  Here is a quick test of S&P500 returns under different IV-HV regimes going back 3000 bars (days). Again the standard  method for my testing uses a 1-year lookback to calculate percentiles :

|   | **Implied Volatility vs Historical Volatility Regimes (IV minus HV)** |
|   | **and next day SPY returns** |  |  |  |   |
|   |  |  |  |  |  | **% positive** | **avg daily** |
|   | **CAGR** | **StDev** | **Sharpe** | **R-squared** | **DVR** | ** days** | **return** |
| Below Median | -(2.77%) | 15.30% | -0.18 | 0.2 | -0.04 | 50.70% | -0.01% |
| Above Median | 3.37% | 16.30% | 0.21 | 0.28 | 0.06 | 54.30% | 0.04% |
| 75th Percentile | 2.83% | 13.00% | 0.22 | 0.46 | 0.10 | 55.41% | 0.06% |
| 25th Percentile | -(1.32%) | 12.20% | -0.11 | 0.003 | 0.000 | 51.43% | -0.01% |

The conclusion is fairly obvious- returns the next day for the SPY (P&P500)  risk-adjusted are higher when implied volatility is higher than historical volatility. The significance of this division, is that half the time, returns are expected to be negative under low IV/HV regimes, and thus this variable is a significant indicator to pay attention to. Based on the finance research  the theory is that implied volatility should subsumes the information contained in historical volatility because it is forward-looking. However, implied volatility is not highly accurate and can be volatile, thus comparing it to historical volatility should provide  a smoother basis for judgement. The residual difference between IV and HV should be more accurate in explaining future returns than historic volatility or implied volatility. Since volatility is  expected to be predictably cyclic,  high residual vol should be followed by lower future vol and vice versa. But what about the impact on mean-reversion strategies? Does high IV vs HV forecast higher or lower returns to a mean-reversion strategy? Lets consider how daily follow-through MR performs under different IV-HV regimes. The same time period and methodology was used as the first test:

|   | **Implied Volatility and Historical Volatility Regimes (IV minus HV) ** |
|  | **and Daily Follow-Through MR returns on SPY (last 3000 bars)** |
|   |   |   |   |   |   | **% positive** | **avg daily** |
|  | **CAGR** | **StDev** | **Sharpe** | **R-squared** | **DVR** | ** days** | **return** |
| Baseline Daily FT MR | 10.10% | 22% | 0.45 | 51% | 0.2295 | 51% | 0.05% |
| Below Median | -(1.10%) | 15.00% | -0.075 | 11% | -0.0082 | 49.90% | 0.00% |
| Above Median | 11.90% | 16.30% | 0.73 | 66% | 0.4818 | 52.40% | 0.10% |
| 75th Percentile | 9.00% | 13.00% | 0.687 | 90% | 0.6183 | 54.40% | 0.15% |
| 25th Percentile | 3.00% | 12.20% | 0.245 | 30% | 0.074 | 51.70% | 0.06% |

Looking at this we see a huge difference in the performance of mean-reversion in different residual volatility regimes (IV-HV). Results are superior to looking at historical volatility in isolation. In fact, when the difference between IV and HV is above the median, daily follow through MR was actually higher returning on both an absolute and risk adjusted basis than the baseline strategy. Thus, you could make greater  returns and much less risk and be in the market roughly 50% of the time. That is a **huge** improvement. The best risk/reward was to trade daily follow-through when IV-HV was in the 75th percentile as it had the highest measure of DVR (R-squared of the equity curve times the sharpe ratio). In this case, your equity curve was straight as an arrow, and you made 90% of the baseline strategy returns in 25% of the time. Money was lost investing in daily follow-through when IV-HV was below the median. Furthermore, the equity curve was terrible with an R-squared of  11%. You would have been better off simply shorting the market in this scenario on an absolute and risk adjusted basis. There are of couse better strategies to take advantage of this, but i will save that for later.

Conclusion: IV-HV  is a very signficant moderator of mean-reversion returns and should be considered when deciding to continue using daily follow-through MR within certain regimes. The explanation for this phenomenon i will leave for   the volatility experts such as Condor Options, or Bill Luby to consider more thoroughly. My take is that IV-HV is a good forecast of future choppiness because it is essentially a reasonable forecast of future volatility. Choppiness is essential for mean-reversion strategies to be effective.
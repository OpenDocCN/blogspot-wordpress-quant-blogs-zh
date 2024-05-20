<!--yml
category: 未分类
date: 2024-05-12 18:50:23
-->

# Moderators of Daily Follow Through MR: Volatility (Part 1 of 3) | CSSA

> 来源：[https://cssanalytics.wordpress.com/2009/08/24/moderators-of-daily-follow-through-mr-volatility-part-1-of-3/#0001-01-01](https://cssanalytics.wordpress.com/2009/08/24/moderators-of-daily-follow-through-mr-volatility-part-1-of-3/#0001-01-01)

**Note:** Detailed backtest reports for the Donchian Channel series can be found on the website built by Corey Rittenhouse: [http://www.catallacticanalysis.com/](http://www.catallacticanalysis.com/) Check it out!

Today we will take a look at one of the different factors that affect the performance of a standard daily follow-through mean-reversion strategy. As a refresher, the strategy assumes that you buy after down days, and go short after up days. Since early 2000, mean-reversion following up or down days has been the dominant paradigm in financial markets–especially for the broad market indexes. This is also a very good proxy for how well other short-term MR indicators such as RSI2 or DV2 will perform under similar circumstances.

Historical volatility will be addressed in this post, and tommorow we will take a look at implied volatility as well. Finally, in subsequent posts, i will combine these factors to have a better understanding of their impact on classic daily follow-through MR. Broadly, this series of posts will also cover the impact of volume as well as the impact of trend strength or R-squared. I will combine all of these factors to create a matrix that helps better predict when to bet on mean-reversion and when to bet on continuation from today’s closing direction in the market. This will help disentangle the sources of MR returns, and also broaden our understanding of how today’s market is functioning.

The first test I ran was on the impact of historical volatility on the daily follow-through MR.  I used 3000 bars of data on the SPY (S&P500) as a test sample ending last week. I classified high volatility as being in the 75th percentile, and low volatility as being in the 25th percentile, both with a lookback of 1-year. Average volatility was anything that fell in between those two levels. For comparison, i used both 10-day and 100-day historical volatility. Here are the results:

|   | **CAGR** | **Sharpe** | **% correct** | **avg daily ret** |
| **High 10d Volatility** | **7.32%** | **0.45** | **52.60%** | **0.126%** |
| High 100d Volatility | 5.28% | 0.32 | 51.00% | 0.087% |
| Average Volatility | 0.62% | 0.03% | 50.30% | 0.013% |
| Low 10d Volatility | 2.25% | 0.29 | 51.00% | 0.036% |
| Low 100d Volatility | 1.47% | 0.18 | 51.20% | 0.025% |

It is immediately obvious that high volatility is far more favorable for the daily follow-through MR strategy. In contrast, the worst environment for daily follow through is the average volatility environment, followed by environments with low volatility. 10-day volatility was a far more superior moderator of returns than the 100-day lookback.  It pays to wait for short-term volatility to bet on mean-reversion, and at present historical volatility is in the 17th percentile. When volatility is low, the return to following the long term trend (1-year average) is superior to daily follow through MR. This suggests that continuation is more probable than reversion on balance, even though the market is overbought on a variety of metrics.

In the second test, i compared what happened in the contingency when the 10-day volatility was lower or higher in relation to the 100-day volatility over the past year in different volatility regimes. I took the 10-day minus the 100-day and looked at the percentile ranking of the difference over the past year (technically above/below average is actually the median).

|   | **CAGR** | **Sharpe** | **% correct** | **avg daily ret** |
| High Vol + Below Avg 10d/100d | 1.50% | 0.38 | 59.00% | 0.30% |
| High Vol + Above Avg 10d/100d | 5.74% | 0.37 | 52.00% | 0.11% |
| Low Vol + Above Avg 10d/100d | 1.05% | 0.38 | 53.60% | 0.09% |
| Low Vol + Below Avg 10d/100d | 1.18% | 0.16 | 50.40% | 0.03% |

It seems apparent that in high volatility environments, follow-through returns are more consistent when the 10-day is lower in relation to the 100-day–ie you want to buy high volatility environments when volatility is slowing down. In contrast, in low volatility environments you want to buy when volatility is speeding up. Logically this makes sense, as it is risky to fade market direction into high and accelerating volatility, and also it is risky to fade extremely quiet markets (low volatility, low 10d/100d vol)  which are prone to major breakouts/breakdowns.

In conclusion, historical volatility and the relationship between short-term and long-term volatility is an important moderator of daily follow through MR returns. A simple contigency matrix can help traders better understand when it is likely to work, and when it is not reliable.
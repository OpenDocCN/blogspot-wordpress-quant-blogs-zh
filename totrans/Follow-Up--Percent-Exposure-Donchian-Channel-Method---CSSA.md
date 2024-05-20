<!--yml
category: 未分类
date: 2024-05-12 18:50:45
-->

# Follow-Up: Percent Exposure Donchian Channel Method | CSSA

> 来源：[https://cssanalytics.wordpress.com/2009/08/19/follow-up-percent-exposure-donchian-channel-method/#0001-01-01](https://cssanalytics.wordpress.com/2009/08/19/follow-up-percent-exposure-donchian-channel-method/#0001-01-01)

One of our more astute and diligent readers- Corey Rittenhouse- actually backtested the Percent Exposure Donchian Channel Method mentioned in my earlier Quick Take article on the subject.  I will make the more detailed and nicely-presented PDF created by Corey available shortly.  For now I will present a brief summary. As a point for new readers–Quick Take articles are simply ideas to help inspire system developers that I have not had a chance to test.  Thus, I had no idea whether the system would actually work in practice.  Nonetheless,  the system concept was designed based on  sound logic and theory–which is a key ingredient in system design. Corey created a  summary of the results for the last 25 years tested on the following futures markets: ES, NQ, TF, GC, SI, HG, CL, HO, NG, RB, ZC, CC,CT, KC,ZW, LE, HE, ZS, SB, GBP, AUD, JPY, EUR, CHF. This is essentially a diversified basket of stock indices, commodities, currencies and fixed income futures which helps to verify robustness.

|   | Summary Stats |   |
| CAGR | StDev | Sharpe | Equity Curve R-squared |  DVR (R-square x sharpe) |
| **12.70%** | 14.10% | 0.83 | 88% | **0.73** |

| % Profitable | Average winner |   |   |
| trades | /average loser | Worst month | Worst year | Max Drawdown |
| 31% | 3.22 to 1 | -12% | -13% | 31% |

Here is a year by year return history separated into two 10-year periods- 1999-2009, and 1988-1998:

| 2009 | 2008 | 2007 | 2006 | 2005 | 2004 | 2003 | 2002 | 2001 | 2000 | 1999 |
| -1% | 50% | -2% | 24% | -13% | 6% | 29% | 11% | -1% | 20% | 0% |

| 1998 | 1997 | 1996 | 1995 | 1994 | 1993 | 1992 | 1991 | 1990 | 1989 | 1988 |
| 11% | 5% | 28% | 5% | 13% | 10% | 13% | -3% | 23% | 13% | 14% |

Here is a breakdown of the percentage of markets showing a profit for the system. This helps to verify robustness:

| **Long Only** | # of Markets | % of Markets |
|   | showing a profit |  Profitable |
| Small Channels (lowest bet size) | 16 | 67% |
| Medium Channels (medium bet size) | 18 | 75% |
| Larger Channels (full bet size) | 20 | 83% |

| **Short Only** | # of Markets | % of Markets |
|   | showing a profit |  Profitable |
| Small Channels (lowest bet size) | 14 | 58% |
| Medium Channels (medium bet size) | 14 | 58% |
| Larger Channels (full bet size) | 16 | 67% |

The annual returns of nearly 13% are fairly solid and likely superior to any buy and hold benchmark. The sharpe ratio of .83 is very solid, especially for a trend following strategy. Returns soared to 50% in 2008 while the world was melting down—displaying the positive kurtosis of trend-following strategies.  Looking at the system from a risk-adjusted perspective, the Percent Exposure model shines. This is to be expected, as bet-sizing is adjusted for the channel breakout length and whether a trade is going with or against the long-term trend. A standard deviation of 14% is lower than both the S&P 500 and the commodity index. Furthermore, the max drawdown of 31% is lower than typical trend following strategies that trade both long and short. The worst month of -12% was tolerable even as a hedge fund strategy. The worst year of -13% was also very low for a trend-following strategy. The equity curve was very smooth with an R-squared of 88%, but becoming a little choppier in recent years as mean-reversion has become the dominant strategy. Finally, the system seems to be effective across a very wide range markets–especially on the long side.

Without going too deep into scrutinizing the results, I would have to conclude that the  Percent Exposure Donchian Channel system is 1) fairly robust 2) a good  risk-adjusted trend following system. There are several ways to improve upon it, while still keeeping robustness intact. Here are some suggestions:

1) Combine the Percent Exposure system with two momentum systems:   **RS Momentum:**  Buy only the top 3 markets ranked by a combination of 12-month price return and 1-month price return (12month rank + 1month rank)/2 .  **Contrarian Momentum:**  For a contrarian bent, you could buy the bottom 3 markets ranked by 3-year price return.  Note that for short signals you would reverse this criteria for both momentum and contrarian. This should raise the returns on an absolute and risk-adjusted basis.

2) Use a trend and volatility filter:  Only take signals if the ADX is greater than 25 or 30\. Or you can use the R-squared of closing prices over the last 20 days as a proxy with a minimum value of 50%. As a volatility filter, only take signals if the 10-day ATR/ 10-day average price is below the 50th percentile over the last year. *A signal is triggered only if it meets both of these criteria.* These numbers have been chosen arbitrarily, but parameter testing should help you find more suitable thresholds.
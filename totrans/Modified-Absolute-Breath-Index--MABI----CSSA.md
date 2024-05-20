<!--yml
category: 未分类
date: 2024-05-12 18:43:58
-->

# Modified Absolute Breath Index (MABI) | CSSA

> 来源：[https://cssanalytics.wordpress.com/2009/10/27/modified-absolute-breath-index-mabi/#0001-01-01](https://cssanalytics.wordpress.com/2009/10/27/modified-absolute-breath-index-mabi/#0001-01-01)

*Note: I am current a humble member (im the “bat-boy” in this crew) of what I can best characterize as an “All-Star” team of  popular bloggers and traders that give you an actionable consensus  market outlook for the next day 10-15 minutes before the close. With Jeff Pietsch of Market Rewind, Rob Hanna of Quantifiable Edges, Michael Stokes of MarketSci, Bob Barnes of BZB Trader, Frank of Trading the Odds, and Rennie Yang of Market Tells—I’m just happy I get to see the masters at work for free! All of these guys have a great track record, and in my opinion every one has something unique to bring to the table. I just helped in designing an adaptive algorithm to dynamically allocate  to the better risk-adjusted performers in the current market regime. (Of course, I also participate and use my own little private machine to assist in generating outlooks.) Thus you not only get the all-star team, you get to back the best hitter! Check us out:* [http://www.quantwizards.com/members/home.php](http://www.quantwizards.com/members/home.php)

Norman Fosback wrote a classic book called “Stock Market Logic” and even though it was published several decades ago, it is still a classic that is applicable even today. Mr. Fosback was an econometrician by training and he seemed to have a very rare combination of creativity , quantitative horsepower, and common sense. In one of his chapters he discusses the “Going Nowhere” Indicators which are based on market breadth. The underlying premise is that one can derive useful information from a market that is “going nowhere.” The rationale is that markets tend to bottom quickly, but form tops over long periods of time. Surprisingly this hypothesis concerning differential velocity in bull versus bear markets holds true even today:  bull markets show long protracted rises, and bear markets demonstrate short and sharp declines followed by wild rallies.

***During bull markets when tops are forming,*** ***the market should theoretically churn with neither advancers or decliners gaining the “upper hand” for long periods of time.*** Think of this process as a sort of stalemate in a tug of war between the bulls and the bears. The Absolute Breadth Index was constructed using weekly data and took the 10-week average of the absolute value of the difference between advancers and decliners divided by total issues traded. High readings over 40% are supposed to be bullish and readings under 15% are supposed to be bearish. This approach worked well for a while, but became inconsistent only because the relative frequency of readings changed over time. The  method of “stipulating absolute levels” with respect to technical indicators is something I am definitely not a fan of and the Modified Absolute Breadth Index (MABI)  takes this correction into account. For my twist on the index, I take a daily vs weekly reading of the differential, and take the 50-day average. I then use the PERCENTRANK function with a lookback of 4 years to encompass an average cycle of the average differential. Lets take a look at the results:

| **MABI and Market Performance Last 9000 bars** |   |   |
|   |   |   |   |   |   |
| MABI Indicator | CAGR | StDev | Raw Sharpe | W% | avg ret/bar |
| > .5 | 5.30% | 15% | 35% | 53.2 | 0.048% |
| <.5 | 1.70% | 9% | 20% | 51.8 | 0.018% |
|   |   |   |   |   |   |
| **MABI and Market Performance Last 3000 bars** |   |   |
|   |   |   |   |   |   |
| MABI Indicator | CAGR | StDev | Raw Sharpe | W% | avg ret/bar |
| > .5 | 4.70% | 20% | 23% | 53.3 | 0.035% |
| <.5 | -(3.50)% | 8% | -(42)% | 49.6 | -(0.054)% |

As you can see, the MABI indicator seems to be able to accurately seperate good and bad periods in the market over the last 35 years, and performance is actually getting better over the last 3000 bars.  When MABI was lower than .2 the market did even worse, while readings far above .5 were more inconsistent. Nonetheless the primary purpose of MABI is to be an uncorrelated indicator to help identify intermediate to longer term tops and bottoms. It is almost like holding a stethoscope to the market to listen to its heartbeat.  Based on extensive testing MABI does a very good job of detecting divergences, and gives information that is definitely not contained in standard indicators. As you might notice “bullish” periods have higher standard deviations simply because they often occur in downtrends, in contrast “bearish” periods have lower standard deviations because they often occur in uptrends. As we will see tommorow in the next post, ***MABI can be the basis of some very profitable short entries*** ***above the 200 ma!***
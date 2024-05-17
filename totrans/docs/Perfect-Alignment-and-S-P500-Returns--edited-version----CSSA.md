<!--yml
category: 未分类
date: 2024-05-12 18:37:15
-->

# Perfect Alignment and S&P500 Returns (edited version) | CSSA

> 来源：[https://cssanalytics.wordpress.com/2010/01/21/perfect-alignment-and-sp500-returns/#0001-01-01](https://cssanalytics.wordpress.com/2010/01/21/perfect-alignment-and-sp500-returns/#0001-01-01)

NOTE: A reader caught a clerical error made in the table…..it should have read Nasdaq leads the NYSE as mentioned in the text of the article etc this has been changed to the correct version

There has been a lot of interesting discussion these days about the power of relative index returns to predict S&P500 performance. Previous research that I displayed suggests that the Russell and S&P500 relationship is also moderated by the VIX, and MarketSci decided to take this one step further by introducing a market-neutral pairs strategy that was quite interesting  [http://marketsci.wordpress.com/2010/01/20/vix-based-pairs-trading-market-neutral-strategy/](http://marketsci.wordpress.com/2010/01/20/vix-based-pairs-trading-market-neutral-strategy/). I will be expanding on this research in subsequent posts. But for now, its time to take a step back before going forward and I realized that further integration with existing findings was necessary. Readers are encouraged to read a classic post by Rob Hanna of Quantifiable Edges about the use of the NYSE/Nasdaq relationship to time the S&P500 [http://quantifiableedges.blogspot.com/2009/05/simple-powerful-timing-indicator.html](http://quantifiableedges.blogspot.com/2009/05/simple-powerful-timing-indicator.html). In a nutshell, when the Nasdaq is outperforming the NYSE, the S&P500 does extremely well–and this effect is persistent over a very long period of time. The rationale is that the Nasdaq is a lower quality and more speculative index than the NYSE, and its relative outperformance is a clear sign that sentiment is healthy and money is entering the market.  As mentioned in a previous post, a healthy sentiment is critical for a rising market. Using this timing indicator, the S&P500 has outperformed buy and hold over the test period.

**Index Alignment Theory**

Now a very relevant question is how  this relates to the effect where the S&P500 performs better when outperforming the Russell 2000– otherwise known as the “Generals Lead the Troops.” As previously noted, the S&P/Russell phenomenon is an autocorrelation effect—large caps lead small caps simply because they are the most liquid and the first to receive institutional funds. When the big money wants into the market they start buying the S&P500 stocks–this is the early stage buying which may or may not last. After this inital race to deploy funds, institutions will follow up their intial purchases with investments in smaller stocks that are in the same sector and spread their purchases over time.  Following the early stage S&P buying, if institutions are really confident in the market they will put money in the Nasdaq first because 1) there is more liquidity in these stocks than small caps and 2) a lot more upside than the higher quality NYSE stocks. As this buying process continues and the feedback loop starts taking effect,  institutions will dump their slow-moving NYSE stocks and increase their allocation to Nasdaq stocks to increase their overall portfolio beta. As long as big money is being deployed in liquid stocks while small caps are under-invested (which is signalled by increased relative performance via the Russell) it is likely that the bull market is still in its early stages. In this zone, there is **“perfect alignment”-** the Nasdaq is leading the NYSE and the S&P500 is leading the Russell 2000.  This shows clearly that the market is healthy and risk is presumably very low.

In contrast, in the late stages of a bull move we see the opposite behavior.  When the S&P starts lagging the Russell, presumably the smart money is starting to liquidate their big positions first while retail investors and less-informed institutions are pumping money fast into small stocks. At this point the market is probably topping and is due for a correction at some point in the future. The only problem is that the S&P/Russell is too long-term as an indicator to be a useful warning sign. The key leading indicator of real-liquidation is if the NYSE starts outperforming the Nasdaq in the short-term.  This confirms a general flight to safety as the big money would rather have less downside risk via quality NYSE stocks.  If this happens, its time to run for the hills because the market will probably roll over very soon.

To test this theory, I used a short-term relative strength measure in the form of the difference in 20-day ROC for the Nasdaq vs NYSE. In keeping with previous tests, I used a 252-day (1-year) relative strength measure for the S&P500 vs Russell. Lets look at the returns for the S&P500 with different index alignments:

|   | **S&P500 Returns with Different Index Alignments (5000 bars)** |
|   |   |   |   |   |   |   |
|   |   | Gross |   |   |   |   |
|   | CAGR | Sharpe | avg daily gain | w% | worst day | exposure |
| S&P>Russell (1yr) and | 5.8% | 0.73 | 0.12% | 56.02% | -3.50% | 24.30% |
| Nasdaq>NYSE (20d ROC) |   |   |   |   |   |   |
|   |   |   |   |   |   |   |
| S&P>Russell (1yr) and | 3.4% | 0.39 | 0.07% | 55.40% | -6.80% | 20.00% |
| Nasdaq<NYSE (20d ROC) |   |   |   |   |   |   |
|   |   |   |   |   |   |   |
| S&P<Russell (1yr) and | 0.0% | 0.086 | 0.02% | 52.50% | -6.10% | 30.00% |
| Nasdaq>NYSE (20d ROC) |   |   |   |   |   |   |
|   |   |   |   |   |   |   |
| S&P<Russell (1yr) and | -3.7% | -0.35 | -0.05% | 50.10% | -9.03% | 25.00% |
| Nasdaq<NYSE (20d ROC) |   |   |   |   |   |   |
|   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |

As you can see, when the indexes are in perfect alignment–a rare condition that happens only 25% of the time– the S&P500 performed very well with nearly a 6% CAGR (vs 6.2% for buy and hold) and with an excellent gross sharpe of .73 (vs .33 for buy and hold) and your worst day over 2 bear markets was a paltry -3.5% loss. When the S&P500 was leading the Russell but the NYSE/Nasdaq indicator was flashing red, the market still did OK as it was probably an early cycle flight to quality that was temporary. This would be an acceptable area to stay invested, and indeed you earned a respectable 3.4% CAGR with slightly better risk-adjusted return and smaller max daily losses than buy and hold. When the S&P500 was lagging the Russell and but the NYSE/Nasdaq indicator was flashing green, the market was starting to get unhealthy but not quite reading for an immediate rollover. Nonetheless returns were very low-if not non-existent  in this condition and probably not worth the risk to hold on. When the S&P500 was lagging the Russell and the NYSE/Nasdaq indicator was flashing red—look out! The market lost money consistently with a – 3.7%  CAGR, and greater tail risk with high max daily losses than in other periods.

In summary, it appears that index alignment is a potentially useful market timing indicator in isolation. Investors and traders should pay attention to the short-term NYSE/Nasdaq relationship and S&P/Russell long-term relationship to judge the health of the market.
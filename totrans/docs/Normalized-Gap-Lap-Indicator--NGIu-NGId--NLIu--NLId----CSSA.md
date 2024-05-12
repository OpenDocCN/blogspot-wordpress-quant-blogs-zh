<!--yml
category: 未分类
date: 2024-05-12 18:11:45
-->

# Normalized Gap/Lap Indicator (NGIu/NGId, NLIu, NLId) | CSSA

> 来源：[https://cssanalytics.wordpress.com/2011/03/21/normalized-gaplap-indicator-ngiungid-nliu-nlid/#0001-01-01](https://cssanalytics.wordpress.com/2011/03/21/normalized-gaplap-indicator-ngiungid-nliu-nlid/#0001-01-01)

Gaps and Laps were formerly popularized by TradingMarkets: [http://www.tradingmarkets.com/](http://www.tradingmarkets.com/). They represent a means of identifying a type of market pattern that isn’t explicitly captured by other indicators.  Gaps or laps up or down are large price moves that originate on the open and occur on very positive or negative news that catches the market off guard. The following set of definitions apply:

gap down:  today’s open<yesterday’s low

lap down: today’s open< yesterday’s close

gap up: today’s open> yesterday’s high

lap up: today’s open>yesterday’s close

Originally much of the research done on gaps/laps used very specific percentage criteria which was to be used across a wide variety of stocks. Generally speaking the results suggested that one should fade the direction of the gap/lap over the next few days. That is, there was a mean-reversion effect to gaps/laps. The issue that I found with the research was that the % criteria such as: “gap down<-10% then buy”, was not normalized by security which tended to lead to distortions. For a small biotech, this is actually a small gap, while for a large cap stock this is  a major-sized gap. Furthermore, a gap down of -10% in 2008 was commonplace even for large caps, while the equivalent gap for a small/volatile stock would be -50% or more. Thus, this method is begging to be normalized, and this can be done several different ways but we will stick to a simpler example for this post:

NGIup:

1) normalized the gap: take the current gap divided by the 10-day ATR as of yesterday’s close and compare it to all other up gaps divided by their 10-day ATR as at t-1 days from the gap.

2) rank the current normalized gap in relation to at least 50 prior up gaps, this is the NGIup

NGIdown: do the same thing just compare to prior down gaps instead

NLIup: do the same thing just compare to prior laps up instead

NLIdown: do the same thing but just compare to prior laps down instead

Applications:

The normalized gap/lap indicators are ideal for use in identifying how to trade for different types of gap setups. It is recommended that you look at extremes such as >80th percentile, or at the very least>50th percentile/median to conduct your analysis. Don’t have any preconceived notions about how gaps or laps should behave. Research indicates that this can be very much stock specific, and also category specific (ie small cap versus defensive large cap). On balance, there should be a mean-reversion effect, but this will vary depending on whether you are looking at up or down gaps/laps and also the magnitude of the gap/lap and the longer-term trend etc.
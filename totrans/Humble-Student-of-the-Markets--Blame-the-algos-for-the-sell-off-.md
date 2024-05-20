<!--yml
category: 未分类
date: 2024-05-18 03:16:14
-->

# Humble Student of the Markets: Blame the algos for the sell-off!

> 来源：[https://humblestudentofthemarkets.blogspot.com/2015/09/blame-algos-for-sell-off.html#0001-01-01](https://humblestudentofthemarkets.blogspot.com/2015/09/blame-algos-for-sell-off.html#0001-01-01)

I've been pondering the reasons for the US stock market's unusual behavior in this latest panic. In particular, the speed and magnitude of the sell-off has been astounding. Consider the puzzle presented by this hourly chart of the SPX over the last two months.

In early July, the market sold off and fear gauges rose. VIX term structure inverted and NYSE TRIN spiked above 2 (blue circles), which triggered two of the three components of my Trifecta Bottom Model (see the chart in

[Is this the Ashley Madison market panic?](http://humblestudentofthemarkets.blogspot.com/2015/08/is-this-ashley-madison-market-panic.html)

). The Trifecta Model has had a 100% record of spotting short-term bottoms since 2010, but it failed in August 2015.

On Friday, August 21, 2015, similar market conditions prevailed. The market had become oversold, according to RSI(21), VIX term structure had inverted, which indicated rising fear, TRIN had risen above 2 and the SPX had tested a key support level at 2020\. These were the classic conditions for an oversold market. Instead of rallying, or even pausing at about the 2040 level, the SPX proceeded to crater over 100 points in the next few days.

Why?

One clue came from the elevated levels of NYSE TRIN (circled in red), which had the characteristics of forced, price-insensitive selling.

It is time to blame the algos.

**Algos for newbies**

An algorithm, or algo, is simply a recipe for doing a certain task. Here are some simple examples of simple algos that would result in forced selling:

*   Margin accounts are required to maintain sufficient equity. If the value of the assets in the account falls below a key level, we ask the account holder to come up with more cash to maintain minimum equity levels. If he can't, we take control of the account and sell the assets.
*   A firm targets a certain Value-at-Risk (VaR) for its capital commitment. When VaR falls because volatility is low, traders are free to (and possibly encouraged) to lever up their allocation. When VaR rises, traders are required to scale back their positions.

During the Crash of 1987, portfolio insurance algos, which had become extremely popular at the time, exacerbated the downside volatility once the selling had started. For the uninitiated, you can replicate a long stock-long put option position with delta hedging. Unfortunately, delta hedging required that you buy stock when it goes up and sell stock when it goes down. So when the market tanked, the portfolio insurance programs (algos) were forced to sell stock, which pushed prices down, which forced them to sell more stock...

**The algo culprits**

Today, delta hedging is not a big part of the market, but others have stepped in to take their place to heighten market volatility. First, there were the HFT algos, which created a minor level of havoc in ETF pricing on Monday, August 24, but HFTs cannot take all of the blame. Marko Kolanovic, JP Morgan quant, explained the violent selling in the context of an unwind from three main types of strategies (via

[Zero Hedge](http://www.zerohedge.com/news/2015-09-03/jpm-head-quant-back-new-warning-only-half-selling-completed-expect-downside-price-ri)

, emphasis added):

> **Volatility Targeting (VT)** Strategies follow fast signals (such as short term realized volatility) and rebalance quickly (e.g. 1-5 days). ***Selling pressure from these strategies (estimated to be $50-75Bn) peaked last week and is largely out of the way now.*** Short-term realized volatility increased from ~10% to ~30%, indicating these funds already reduced their exposure by ~70%. If volatility were to increase further (e.g. in-line with the peak realized volatility in 2011 of ~50%), these funds would have to sell progressively smaller amounts (e.g. an additional ~10-15%). The question is when these funds will start buying. Our view is that the re-levering of these funds is not imminent (e.g. not in the next few days). Leverage in these strategies is a function of trailing volatility (e.g. moving average of the VIX or 1M realized volatility), and even if the VIX were to start declining now, trailing realized volatility would stay elevated for the next ~3 weeks.
> 
> **CTAs** – Following our report last week, we have been getting questions about CTA equity exposure and the timeline of CTA flows. Our CTA replication models suggested that CTA equity exposure at the end of July was very high, at approximately 30% (or $80-$100Bn notional). This allocation to equities is also consistent with the performance of CTA indices in August (Bonds and Commodities were roughly flat, while Equities were down 8% - thus, a 30% equity allocation would match the -2.5% CTA observed performance). As the trend following signals (e.g. 1M, 3M, 6M, 12M price returns) started turning negative in August, CTAs started de-levering equities (in early August). As of September 1st, our CTA replicator indicates that the strategies should be ~25% short equities (short ~$70bn). This would indicate a ~$150bn swing (selling) of CTAs’ equity allocation.
> 
> However, CTA strategies don’t rebalance as quickly as VT strategies, and it often takes 1-4 weeks to achieve their target exposure. To assess where we are in the process of CTA de-leveraging, we have calculated the daily beta of a broad CTA index (HFRXSDV) to the SP 500 shown in the figure below. Note that the CTA SP 500 beta dropped from record levels at the beginning of August to zero currently, indicating that CTAs may have completed more than 50% of the expected equity selling (as noted above, target equity exposure is negative ~25%). ***We estimate that CTAs may continue selling equities for another ~2 weeks, and that the flows may total ~$40-$60bn.*** Once CTAs establish their September 1st target positions (short equities), they will no longer be selling, and risk becomes skewed towards CTAs buying equities. We estimate CTA flows in other asset classes include a reduction of USD exposure (from $40bn to zero), no change in bond positions, and some short covering of Oil and Gold (from short 40bn to short 30bn).
> 
> **Risk Parity (RP)** –We studied this allocation method in our Primer on Systematic Strategies, and argued that it is one of the soundest approaches to managing portfolio risk.
> 
> Risk Parity strategies de-lever when asset volatility and correlation increase. In our report last week, we estimated that risk parity outflows from equities may total $50-100bn on account of the increase in market volatility and risky asset correlations. These rebalances have started, but, given their typically slower rebalance frequency (e.g. monthly), are largely incomplete. ***We believe the bulk of the risk parity flows are yet to come, and this may add selling pressure to equities over the next 1-3 weeks.*** To illustrate this point, one can look at a sample multi-asset Risk Parity strategy such as the Salient Risk Parity index. The beta of this index to the SP 500 (shown in the figure above) reached highs of 60% in early August, and has dropped to about 45% currently (compared to a beta of 0% during some of the previous episodes of market volatility).
> 
> Please note that in our estimate of Risk Parity assets we have included funds that use Risk Parity as a risk management overlay and tactical allocation, and not just the dedicated Risk Parity (Quant) hedge funds. One could perhaps even broaden the definition of Risk Parity funds to include investors that change their strategic allocation based on expected volatility (e.g. such as CalSTRS announcement of plans to reduce equity exposure in the near future, recently reported in the media).

Kolanovic's main conclusion as of September 3, is to expect more selling:

> In summary, ***we estimate that only about half (or slightly more than half) of total technical selling was completed to-date (mostly completed by VT funds, half by CTAs, and a smaller fraction by RPs). We estimate that a further ~$100bn of selling remains to be completed over the next 1-3 weeks.*** As a result, we expect elevated volatility and downside price risk to persist. In our view, the risk/reward for equity investors remains in favor of waiting, rather than being fully invested until there is more clarity from macro data and central banks.

Risk-parity strategies have been the focus as the cause of the selling. Here is the view from BoAML (via

[Business Insider](http://www.bloomberg.com/news/articles/2015-09-01/bank-of-america-crunches-the-numbers-on-summer-s-quant-storm)

):

> Bank of America Merrill Lynch equity derivatives strategists, led by Chintan Kotecha, who write that "Risk parity is not the risk, vol[atility] control is." As they note, it's worth differentiating between risk parity investors with a fixed amount of leverage, and those who tie the amount of leverage applied to their portfolios to market volatility. The latter begin life with a target portfolio volatility level and then apply a certain amount of leverage to their portfolio based on their forecast of future portfolio volatility. An easy example used by BofAML is two times leverage applied to a portfolio with a target volatility of 10 percent and expected to have a volatility of 5 percent. Conversely, a portfolio with forecast volatility of 20 percent could achieve a target volatility of 10 percent by deleveraging its portfolio to 0.5 times levered.

BoAML went on to explain that the amount of selling is a function of how the risk-parity strategy is implemented and the level of leverage allowed in the strategy:

> If the leverage applied to risk parity is via target volatility, then the change in component allocations due to dynamically adjusting the portfolio’s leverage could potentially lead to a collective significant deleveraging of assets tracking risk parity. The amount of deleveraging will be a function of the fund’s target volatility and maximum leverage allowed. But more significantly, the deleveraging will also be a function of the prevailing volatility prior to the volatility spike and the magnitude of the daily moves within the volatility spike. There are a variety of different target volatility levels and leverage caps that are often applied by risk parity funds. Typically, they tend to target a volatility level between 6 percent to 10 percent with maximum leverage ranging from 1.5x to 3.0x.
> 
> Regardless of the target volatility and max leverage limits within a risk parity fund, however, the recent and unusually violent spike in equity volatility from depressed levels ... alongside a relatively muted diversification benefit from fixed income ... led to a significant spike in the volatility of, and likely a subsequent deleveraging from, some risk parity strategies.

Here is an example:

> In this hypothetical example the current deleveraging would be the 7th largest (Table 3) but could be the most impactful on markets given the growth in assets tracking risk parity in recent years.

I am not here to bash risk-parity strategies. While naysayers can point to the $80 billion Bridgewater All-Weather Fund, which is a key flagship RP fund, 

[was -4.2% in August and -3.8% YTD](http://www.finalternatives.com/node/31669)

, 

[Ben Carlson](http://awealthofcommonsense.com/in-defense-of-risk-parity-or-any-long-term-strategy/)

 has also correctly pointed out that these strategies have had a terrific long-term record. They have largely worked and done their job (also see this highly useful primer from 

[FT Alphaville](http://ftalphaville.ft.com/2015/08/25/2138210/myths-and-facts-about-risk-parity/)

 on the risk-parity strategy).

**Market implications**

Nevertheless, the latest volatility storm, which was sparked by a number of volatility-related strategies, has a couple of important market implications.

Tactically, Kolanovic's analysis suggests that there will be more equity selling in the next 1-3 weeks, which makes me more comfortable my constructive long-term call on equity market, but a warning of a re-test of the 1820-1870 level on the SPX in the near future (see

[Constructive on stocks, but waiting for the re-test](http://humblestudentofthemarkets.blogspot.com/2015/09/constructive-on-stocks-but-waiting-for.html)

).

Longer term, however, the role played by RP in exacerbating market volatility are likely to reduce their popularity, just as portfolio insurance programs lost some of their shine after the 1987 Crash. There have been many investors warning about the instability created by this class of strategy.

[Leon Cooperman](http://www.marketwatch.com/story/leon-cooperman-says-blame-the-machines-for-market-volatility-2015-09-08)

of Omega Advisors recently complained that the volatility created by "the machines", which include RP, were responsible for his poor performance. Others like 

[Ben Inker](https://www.gmo.com/docs/default-source/public-commentary/gmo-quarterly-letter.pdf?sfvrsn=14)

of GMO, who characterized these strategies as being "price-insensitive investors" who could create wild swings in market prices (emphasis added):

> Another group of price-insensitive investors are managers of risk parity portfolios. These portfolios make allocations to asset classes not with regard to pricing of assets, but rather their volatility and correlation characteristics. Their price-insensitivity comes out in a couple of ways. First, ***as money flows into the strategies, they are levered buyers of bonds and inflation-linked bonds in particular***. Like most strategies, if the money flows out, they are forced sellers of a slice of their portfolio. Second, unlike many other investors, they will also tend to buy and sell based on changes in volatility. ***As the volatility of an asset falls, these strategies will tend to lever it up further, and as the volatility rises they will sell.***

[Bloomberg](http://www.bloomberg.com/news/articles/2015-09-08/mit-quant-guru-andrew-lo-on-market-s-meltdown-august-sucks-)

interviewed leading MIT finance academic Andy Lo, who said that volatility-related strategies are exacerbating market volatility  (emphasis added):

> Question: Are volatility targeting strategies part of the story? Have they become so popular that they’re exaggerating the moves?
> 
> Lo: ***Not only are they exaggerating the moves, but I think they are creating volatility of volatility.*** So it’s making the market quite a bit more complicated and the dynamics now are much more different and much more difficult to manage if you’re not aware of how these dynamics play out.

Lo also believed that RP is becoming a crowded trade:

> Question: ***Is risk parity looking like a crowded trade?***
> 
> Lo: ***I think there’s definitely a case in point of the idea of alpha becoming beta.*** The idea that once you start popularizing a particular investment approach, and it becomes so popular, that in and of itself creates these kinds of shock waves. So for example if the strategy itself underperforms, now we have a larger number of investors that are going to be unwinding that strategy and that will create a kind of cascade effect where the strategy will underperform even more as people start to take money out of the strategy. There are a number of examples. ***Risk parity, of course, is the most recent.*** But before that trend following, before that value investing, growth investing, earnings surprise, earnings momentum, any kind of a strategy can become a crowded trade. And when it does you have to just make sure that the risk premium associated with that trade is commensurate with the potential risks of getting hit with these unwinds.
> 
> Question: Are volatility targeting strategies part of the story? Have they become so popular that they’re exaggerating the moves?
> 
> Lo: Not only are they exaggerating the moves, but I think they are creating volatility of volatility. So it’s making the market quite a bit more complicated and the dynamics now are much more different and much more difficult to manage if you’re not aware of how these dynamics play out.

While the criticism coming from Bridgewater competitors like Cooperman and Inker might be viewed as self-serving, academics like Andy Lo are adding to the chorus that the risk-parity strategy is becoming a case of "alpha turning into beta". This view will prompt the pension and investment consultant community to start to pull back from this investment approach and assets will start to dwindle in the years to come.

This brings up a second important investment implication. My assessment that this was a once in 20 year tail event will likely turn out to be true. We will not see a repeat of the violent downdraft in stock prices caused by these kinds of volatility related strategies, which makes me also comfortable with my assertion that my Trend Model trading strategy was trading off better average returns for tail risk, which happens every 20 years or so (see

[Trend Model August report card: An invaluable lesson in model design](http://humblestudentofthemarkets.blogspot.com/2015/09/trend-model-august-report-card.html)

).

In 20 years, the lessons from this volatility storm will be forgotten and a new generation of quants and financial engineers will have dreamed up other ways to crash the market.
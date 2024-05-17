<!--yml
category: 未分类
date: 2024-05-18 07:05:02
-->

# Physics Perspective: High-frequency trading -- the downside, Part I

> 来源：[http://physicsoffinance.blogspot.com/2011/09/high-frequency-trading-downside-part-i.html#0001-01-01](http://physicsoffinance.blogspot.com/2011/09/high-frequency-trading-downside-part-i.html#0001-01-01)

Andrew Haldane of the Bank of England has given a stream of recent speeches -- more like detailed research reports -- offering deep insight into various pressing issues in finance. One of his

[most recent speeches](http://www.bankofengland.co.uk/publications/speeches/2011/speech509.pdf)

looks at high-frequency trading (HFT), noting its positive aspects as well as its potential negative consequences. Importantly, he has tried to do this in non-ideological fashion, always looking to the data to back up any perspective.

The speech is wide ranging and I want to explore it points in some detail, so I'm going to break this post into three (I think) parts looking at different aspects of his argument. This is number one, the others will arrive shortly.

To begin with, Haldane notes that in the last decade as HFT has become prominent trading volumes have soared, and, as they have, the time over which stocks are held before being traded again has fallen:

> ... at the end of the Second World War, the average US share was held by the average investor for around four years. By the start of this century, that had fallen to around eight months. And by 2008, it had fallen to around two months.

It was about a decade ago that trading execution times on some electronic trading platforms fell below the one second barrier. But the steady march to ever fast trading goes on:

> As recently as a few years ago, trade execution times reached “blink speed” – as fast as the blink of an eye. At the time that seemed eye-watering, at around 300-400 milli-seconds or less than a third of a second. But more recently the speed limit has shifted from milli-seconds to micro-seconds – millionths of a second. Several trading platforms now offer trade execution measured in micro-seconds (Table 1).
> 
> As of today, the lower limit for trade execution appears to be around 10 micro-seconds. This means it would in principle be possible to execute around 40,000 back-to-back trades in the blink of an eye. If supermarkets ran HFT programmes, the average household could complete its shopping for a lifetime in under a second.
> 
> It is clear from these trends that trading technologists are involved in an arms race. And it is far from over. The new trading frontier is nano-seconds – billionths of a second. And the twinkle in technologists’(unblinking) eye is pico-seconds – trillionths of a second. HFT firms talk of a “race to zero”.

Haldane then goes on to consider what effect this trend has had so far on the nature of trading, looking in particular at market makers.

First, he offers a useful clarification of why the bid-ask spread is normally taken as a useful measure of market liquidity (or more correctly, the inverse of market liquidity). As he points out, the profits market makers earn from the bid-ask spread represent a fee they require for taking risks that grow more serious with lower liquidity:

> The market-maker faces two types of problem. One is an inventory-management problem – how much stock to hold and at what price to buy and sell. The market-maker earns a bid-ask spread in return for solving this problem since they bear the risk that their inventory loses value. ...Market-makers face a second, information-management problem. This arises from the possibility of trading with someone better informed about true prices than themselves – an adverse selection risk. Again, the market-maker earns a bid-ask spread to protect against this informational risk.
> 
> The bid-ask spread, then, is the market-makers’ insurance premium. It provides protection against risks from a depreciating or mis-priced inventory. As such, it also proxies the “liquidity” of the market – that is, its ability to absorb buy and sell orders and execute them without an impact on price. A wider bid-ask spread implies greater risk in the sense of the market’s ability to absorb volume without affecting prices.

The above offer no new insights, but explains the relationship in a very clear way.

Next comes the question of whether HFT has made markets work more efficiently, and here things become more interesting. First, there is a great deal of evidence (

[some I've written about here earlier](http://physicsoffinance.blogspot.com/2011/08/algorithmic-trading-positive-side.html)

) showing that the rise of HFT has caused a decrease in bid-ask spreads, and hence an improvement in market liquidity. Haldane cites several studies:

> For example, Brogaard (2010) analyses the effects of HFT on 26 NASDAQ-listed stocks. HFT is estimated to have reduced the price impact of a 100-share trade by $0.022\. For a 1000-share trade, the price impact is reduced by $0.083\. In other words, HFT boosts the market’s absorptive capacity. Consistent with that, Hendershott et al (2010) and Hasbrouck and Saar (2011) find evidence of algorithmic trading and HFT having narrowed bid-ask spreads.

His Chart 8 (reproduced below) shows a measure of bid-ask spreads on UK equities over the past decade, the data having been normalised by a measure of market volatility to "strip out volatility spikes."

It's hard to be precise, but the figure shows something like a ten-fold reduction in bid-ask spreads over the past decade. Hence, by this metric, HFT really does appear to have "greased the wheels of modern finance."

But there's also more to the story. Even if bid-ask spreads may have generally fallen, it's possible that other measures of market function have also changed, and not in a good way. Haldane moves on to another set of data, his Chart 9 (below), which shows data on volatility vs correlation for components of the S&P 500 since 1990\. This chart indicates that there has been a general link between volatility and correlation -- in times of high market volatility, stock movements tend to be more correlated. Importantly, the link has grown increasingly strong in the latter period 2005-2010.

What this implies, Haldane suggests, is that HFT has driven this increasing link, with consequences.

> Two things have happened since 2005, coincident with the emergence of trading platform fragmentation and HFT. First, both volatility and correlation have been somewhat higher. Volatility is around 10 percentage points higher than in the earlier sample, while correlation is around 8 percentage points higher. Second, the slope of the volatility / correlation curve is steeper. Any rise in volatility now has a more pronounced cross-market effect than in the past.... Taken together, this evidence points towards market volatility being both higher and propagating further than in the past.

This interpretation is as interesting as it is perhaps obvious in retrospect. Markets have calmer periods and stormier periods. HFT seems to have reduced bid-ask spreads in the calmer times, making markets work more smoothly. But it appears to have done just the opposite in stormy times:

> Far from solving the liquidity problem in situations of stress, HFT firms appear to have added to it. And far from mitigating market stress, HFT appears to have amplified it. HFT liquidity, evident in sharply lower peacetime bid-ask spreads, may be illusory. In wartime, it disappears. This disappearing act, and the resulting liquidity void, is widely believed to have amplified the price discontinuities evident during the Flash Crash.13 HFT liquidity proved fickle under
> stress, as flood turned to drought.

This is an interesting point, and shows how easy it is to jump to comforting but possible incorrect conclusions by looking at just one measure of market function, or by focusing on "normal" times as opposed to the non-normal times which are nevertheless a real part of market history.

As I said, the speech goes on to explore some other related arguments touching on other deep aspects of market behaviour. I hope to explore these in some detail soon.
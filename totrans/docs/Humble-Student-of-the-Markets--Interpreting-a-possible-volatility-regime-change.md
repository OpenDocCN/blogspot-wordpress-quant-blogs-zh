<!--yml
category: 未分类
date: 2024-05-18 03:40:36
-->

# Humble Student of the Markets: Interpreting a possible volatility regime change

> 来源：[https://humblestudentofthemarkets.blogspot.com/2014/04/interpreting-possible-volatility-regime.html#0001-01-01](https://humblestudentofthemarkets.blogspot.com/2014/04/interpreting-possible-volatility-regime.html#0001-01-01)

The job of a good market strategist is to use both

[the right and left brain](http://psychology.about.com/od/cognitivepsychology/a/left-brain-right-brain.htm)

 to analyze the markets. The left brain is usually thought of as the analytical and reasoning side - and investors can always use the reason, rigor and discipline of investment models. The right brain is the creative and intuitive side. Here, investors can benefit from the observation, intuition and experience of the analyst to know when the underlying assumptions of investment model might be going off the rails and make the right kinds of adjustments.

Here is an example of what I have observed from the signals from the equity option market.

**A possible volatility regime change** **Left brain:**

In a previous post (see

[A case of "risk exhaustion"?](http://humblestudentofthemarkets.blogspot.com/2014/04/a-case-of-risk-exhaustion.html)

), I had highlighted a comment from MacNeil Curry of BoAML that the stock market has not seen a meaningful bottom until the VIX spikes above 20 (via

[Zero Hedge](http://www.zerohedge.com/news/2014-04-14/bofaml-warns-vix-complacency-suggest-stocks-fall-further)

):

> Since 2012 most tradable market lows have come only after the VIX has pushed north of 20%. It is currently only 17%.
> 
> In such an environment, US Treasuries should rally further. Indeed, US 10yr yields have broken below key resistance at 2.608%/2.632%, exposing the long term pivot zone of 2.469%/2.399%. The Japanese ¥ should benefit as well. The 200d in $/¥ is key (100.81) A break below would do significant psychological damage and force out many trend followers.

The analysis certainly makes sense, but...

**Right brain:** I was thinking about it was funny that the look-back window only went back to 2012, which was not a very long time. Just for fun, I charted for the last five years the VIX Index  (bottom panel), the equity only put-call ratio (in grey), its 21 day moving average (in blue) and the SPX (red).

True enough, the bottom panel showing the VIX verifies Curry`s observation that the market did not see a tradable bottom until the VIX spiked over 20\. However, that rule would not have worked pre-2012 as the VIX traded at significantly higher levels. It appears that there was a regime change to lower vol in late 2011 or early 2012 and we may be seeing signs of a shift back to higher vol now.

The equity-only put-call ratio seems to provide an early warning sign of such a change. Note how its 21 dma rallied through a downtrend line in early 2011 while the VIX was falling during this period. Soon after, volatility rose dramatically and stock prices rolled over.

Note how we are experiencing a similar pattern of the 21 dma of the equity only put-call ratio rising through a downtrend and a rounding bottom in the 21 dma. ***This may be an early warning sign that equity volatility is set to rise.***

**Other signs of rising volatility**

There is support for the idea of rising vol. SocGen has noted that hedge funds have changed to buying volatility from being a seller for a prolonged period (via

[FT Alphaville](http://ftalphaville.ft.com/2014/04/02/1819182/end-of-a-low-vol-era/)

). It is interesting that hedge funds turned to be large sellers of vol in late 2011 and early 2012, when the vol regime seemed to have changed:

The SocGen team justified the change this way:

> Somewhat lower levels of volatility recently, combined with a risk of a spike in volatility due to geopolitical tensions with Russia, are likely to have an influence, but alone do not explain the trend. Hence our conclusion that the period of low volatility is coming to an end.

Here is more "color" of the SocGen view, according to this

[Bloomberg](http://www.bloomberg.com/news/2014-04-14/days-of-market-calm-seen-ending-in-hedge-fund-vix-bets.html)

report:

> “You may be seeing the first indications that the days of very low volatility are numbered,” Arthur van Slooten, a strategist at Societe Generale SA, said in a phone interview from Paris on April 11\. “Expectations for rate hikes may become more aggressive when the data from the U.S. starts heating up.”
> 
> While bearish contracts on the VIX have increased in the past two weeks, the level is about half the average from 2012 and 2013\. They are net short 31,746 futures on the gauge, compared with a mean 61,953 in the last two years, data from a Commitment of Traders report by the Washington-based CFTC show.

A simpler explanation may just be a case of hedge funds getting into a crowded short position in volatility:

> U.S. stocks had one of their most tranquil years in 2013 as investors became more confident in the bull market and began returning cash to mutual funds. The VIX averaged 14.3 last year, the lowest level since 2006\. It has fallen more than 18 percent annually in four of the past five years.
> 
> The persistent decline lured hedge funds to short the volatility gauge, which is based on the cost of options on the SP 500\. Large speculators had a record 116,000 net-short positions on VIX futures in August, CFTC data show.
> 
> They’ve all but disappeared as equities suffered the biggest weekly decline in almost two years. Investors are questioning stock valuations as the Federal Reserve reduces stimulus during a strengthening economy.

**Model re-calibration under a regime change**

If there is indeed a change in vol regime, then there are a number of important implications for investors. For one, analysts like MacNeil Curry may have to re-calibrate their models. We may not see a tradable bottom in stocks until the VIX Index rises much higher than just 20.

Other analysis, like this observation from

[Sheldon McIntyre](http://stocktwits.com/message/22151459)

about the VIX-VXV ratio flashing a buy signal may not necessarily be applicable under the new vol regime. The VIX-VXV ratio measures the term structure of volatility and McIntyre observed that when the ratio falls below 0.92, especially if it had inverted (risen above 1), it has been a good buy signal for the stock market:

I had studied this ratio in the past (see

[Waiting for a Santa Claus rally](http://humblestudentofthemarkets.blogspot.com/2012/11/waiting-for-santa-claus-rally.html)

) and came to a similar conclusion as McIntyre. However, a possible change in vol regimes raised some concerns of the "buy when VIX-VXV falls below 0.92" rule. I backtested a simple trading rule based on the VIX-VXV ratio for the last five years. The buy rule is based on the following two conditions:

1.  The VIX-VXV ratio falling below 0.92; and
2.  It had inverted, ratio more than 1, in the recent past.

The results of the backtest are charted below. The black line shows the VIX-VXV ratio, the red line the SPX and the vertical lines are the signals generated by the system. I then classified the signals as being successful (blue vertical line) if the market was higher one month after the signal, while the unsuccessful signals were in red and flat returns colored in black.

**Backtest of VIX-VXV trading system**

Pre-2012, the batting average for this trading system was so-so as all of the red vertical lines occurred during that period. The win-loss-tie rate in the period was 4-3-1, which is ok but not enough to build a trading system from. In the post-2012 period, when vols were much lower, the buy signals showed a 100% win rate.

Now that we have a buy signal from this system but a possible vol regime change, what success rate should be applicable to this latest signal?

**Other implications of a vol regime change**

Since volatility is inversely correlated to stock market returns, another important implication of a vol regime change is the expectation of a correction in stock prices. The recent change in market leadership from growth to value stocks is further evidence of a sea change occurring in the markets.

J.C. Parets at

[All Star Charts](http://allstarcharts.com/money-rotates-late-cycle-names/)

recently highlighted analysis by JC O’Hara from FBN Securities expressing concerns over the shift in sector leadership (emphasis added):

> The recent sector performance has been troublesome. It is not an encouraging sign to see the market being led by utilities. Even more concerning is the lack of performance in Discretionary, Industrials and Financials. The last 90 days we have seen just that. Examining prior market peaks (too early to confirm we are currently at one), we note that Discretionary weakness combined with Utility outperformance was a forewarning of market weakness to come. Smart money hides in Utilities, Staples, Health Care and Energy, while Financials, Discretionary and Technology get hit the hardest. While there has certainly been active sector rotation from 2013, the market has not turned lower yet. ***If the recent sector performance is a canary in the coal mine, we expect to see shallow bounces where traders lighten up on their riskier assets, and continue to rotate money into the historical sectors that held up the best.***

I have observed a similar effect about risk appetite (see 

[Bears 2 Bulls 1](http://humblestudentofthemarkets.blogspot.com/2014/04/bears-2-bulls-1.html)

). I constructed a risk appetite index based on an equally-weighted long position in the NASDAQ 100 and Russell 2000 (high beta risk-on index) minus an equally weighted short position in the defensive sectors of Consumer Staples, Telecom and Utilities (low beta risk-off index). As the chart below shows, risk appetite is rolling over:

What's more, I further created my own composite index of small cap vs. large cap relative performance, consisting of the an equal weighted composite of the Russell 2000, SP 600 small cap index and the equal weighted SP 500 index relative to the SP 500\. The signs of falling momentum in high-beta small cap relative performance (and therefore a regime change) is unmistakable.

What was more disturbing about O’Hara analysis is his historical parallel with the sector market leadership change at the market top in 2007, which also showed a major leadership shift from Financial and Consumer Discretionary to defensive sectors:

A similar pattern occurred at the market peak in 2000:

Parets concluded:

> JC O’Hara sent this over to me at what I think is the perfect time to point out this rotation. This seems all too similar to prior market peaks. We’re going to want to see Financials, Tech and Discretionaries start to turn back up on a relative basis in order to take this scenario out of the equation. But the consistent underpermance out of these sectors and money flow into Utilities and Energy can’t be ignored. The market is speaking. Are you listening?

To be sure, we are not seeing the same fundamental backdrop that could cause the sort of bear markets that began in 2000 and 2007, but I am seeing preliminary signs that earnings growth are starting to face headwinds because of the lack of capex revival (see

[Capex: Still waiting for Godot](http://humblestudentofthemarkets.blogspot.com/2014/04/capex-still-waiting-for-godot.html)

). Nevertheless, these kinds of warning signs of regime shift from changes in sector leadership should not be ignored.

**An out-of-favor strategy**

Finally, if volatility were to increase, investors may wish to consider a highly hated strategy to consider - trend-following managed futures. These strategies have shown

[good long-term results](http://physicsoffinance.blogspot.ca/2014/04/how-to-consistently-beat-market-follow.html)

, but their short-term results have been so terrible that even the legendary hedge fund manager Paul Tudor Jones shut down his managed futures Tudor Tensor Fund after its asset base collapsed (via

[AllAboutAlpha](http://allaboutalpha.com/blog/2014/04/13/what-a-hedge-fund-failure-looks-like/)

):

> The Tensor Fund went from over $1 billion ($1.5 per our numbers) down to *just* $120 million times over the last three years, and that is the reason the fund is closing, not anything to really do with performance, the skill of the manager, or expertise of the team. The closing of Tensor is more of a commentary on investors buying in at the top of a cycle and getting out at the bottom than anything else.

It does appear to be a business decision rather than purely an investment decision. Here is the performance of Tudor Tensor:

Longer term, the numbers looked ok:

Now consider the fact that trend following models have an implicit long-volatility bet (see analysis via 

[Attain Capital Management](http://managed-futures-blog.attaincapital.com/2013/08/06/forget-the-vix-look-at-global-market-volatility/)

). This chart tells the story by defining volatility as global volatility rather than just VIX:

Today, we have an instance of a hated strategy that has been abandoned by investors and a possible regime change that favors that strategy. What more could you ask for?

**Left and right brained analysis**

The bigger point I am trying to make here is that experienced quantitative analysts have to combine both their left and right brains to make investment processes that create alpha. You can't simply rely on models that have worked in the past, you have to use your observation, intuition and market experience in knowing how to use those models.

I may be wrong on this, but I am seeing evidence of a regime change going on in the markets. Volatility is poised to rise and sector leadership is shifting. Are you and your models prepared?

*Cam Hui is a portfolio manager at [Qwest Investment Fund Management Ltd.](http://www.qwestfunds.com/) (“Qwest”). The opinions and any recommendations expressed in the blog are those of the author and do not reflect the opinions and recommendations of Qwest. Qwest reviews Mr. Hui’s blog to ensure it is connected with Mr. Hui’s obligation to deal fairly, honestly and in good faith with the blog’s readers.”

None of the information or opinions expressed in this blog constitutes a solicitation for the purchase or sale of any security or other instrument. Nothing in this blog constitutes investment advice and any recommendations that may be contained herein have not been based upon a consideration of the investment objectives, financial situation or particular needs of any specific recipient. Any purchase or sale activity in any securities or other instrument should be based upon your own analysis and conclusions. Past performance is not indicative of future results. Either Qwest or I may hold or control long or short positions in the securities or instruments mentioned.*
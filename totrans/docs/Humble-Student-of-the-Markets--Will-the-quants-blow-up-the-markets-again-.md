<!--yml
category: 未分类
date: 2024-05-18 03:19:31
-->

# Humble Student of the Markets: Will the quants blow up the markets again?

> 来源：[https://humblestudentofthemarkets.blogspot.com/2015/06/will-quants-blow-up-markets-again.html#0001-01-01](https://humblestudentofthemarkets.blogspot.com/2015/06/will-quants-blow-up-markets-again.html#0001-01-01)

Josh Brown had a fascinating 

[post](http://thereformedbroker.com/2015/06/21/are-quants-the-new-systemic-risk/)

 which postulated that the quants pose a significant systemic risk to market volatility:

> There’s an interesting idea going around that asset management – specifically the metastasizing quantitative strategies run via black box are where the next big scare is due to come out of. Volatility has been so low, for so long, that winning trades have become crowded and leverage is bountiful. And the kicker – they’re all running the same playbook, loading up in the same trades.

Josh referred to a post by Dominique Dassault at

[Global Slant](http://globalslant.com/2015/06/black-box-trading-why-they-all-blow-up/)

and he drew the conclusion that it may all collapse as it did in 2008:

> Dassault, in referring to “ten years ago”, is referencing the subject of [Scott Patterson’s excellent book, *The Quants*](http://www.amazon.com/gp/product/0307453383/ref=as_li_tl?ie=UTF8&camp=1789&creative=390957&creativeASIN=0307453383&linkCode=as2&tag=cityhammercom-20&linkId=GKUFGMGRKH4LSCKG), in which a handful of genius mathematicians were blown up in a 2006 incident which presaged the global market meltdown that would begin a year later.

I think that Josh missed the point. The incident that Dassault referred to was not the crash of 2008, in which quants made erroneous assumptions about their model inputs (house prices don't fall). Instead, she was referencing a little known quant meltdown that which occurred in August 2007 in which equity quants got into a crowded trade when someone tried to liquidate - in size. I wrote about this episode before (see

[Are quants the victims of their own success?](http://humblestudentofthemarkets.blogspot.com/2008/01/are-quants-victims-of-their-own-success.html)

). The chart below shows the HFRX Equity Market Neutral Index (in blue) and a different strategy (in red) that I was involved in which used some very different factors that did not land us in the crowded long.

From discussions with former colleagues and other equity quants at the time, the meltdown was very ugly. Long-only quantitative accounts with relatively low turnover portfolios suddenly saw relative performance tank to -10% to -15% against their benchmarks in a matter of days, as per the above chart. Moreover, factors that were uncorrelated by design, e.g. value vs. growth, all suddenly saw their return correlations converge to 1.

**How models blow up**

Dassault explained the fatal design flaw of these models in her blog. She had been interviewing with a leading hedge fund manager about 10 years ago who expressed concerns about the stability of quant models:

> While in Greenwich Ct. one afternoon I will never forget a conversation I had with a leading quantitative portfolio manager. He said to me that despite its obvious attributes “Black Box” trading was very tricky. The algorithms may work for a while [even a very long while] and then, inexplicably, they’ll just completely “BLOW-UP”. To him the most important component to quantitative trading was not the creation of a good model. To him, amazingly, that was a challenge but not especially difficult. The real challenge, for him, was to “sniff out” the degrading model prior to its inevitable “BLOW-UP”. And I quote his humble, resolute observation “because, you know, eventually they ALL blow-up“…as most did in August 2007.
> 
> It was a “who’s who” of legendary hedge fund firms that had assembled “crack” teams of “Black Box” modelers: Citadel, Renaissance, DE Shaw, Tudor, Atticus, Harbinger and so many Tiger “cubs” including Tontine [not all strictly quantitative but, at least, dedicated to the intellectual dogma]…all preceded by Amaranth in 2006 and the legendary Long Term Capital Management’s [“picking up pennies in front of a steam-roller“] demise one decade earlier.

My circle of quants at the time of the August 2007 were not the Citadels and DE Shaws, but traditional long-only quant shops around Boston like SSgA, GMO and so on. The results were the same. Everyone blew up.

At the time, most of the equity quants more or less had the same approach to modeling, though the details of the models were different. They were multi-factor models with a little bit of growth, a little bit of value, sprinkle in some momentum (fundamental in the form of estimate revision and earnings surprise), technical in the form of PRICE momentum, usually some form of relative strength with a one-month price reversal. They might toss in other exotic ingredients like insider trading activity or buybacks. These multi-factor models used uncorrelated factors by design, so that when you combined them, they were supposed to give you a stable alpha.

Then they overlaid extensive risk control. Dassault explains what she saw at her hedge fund:

> First of all, a large number of variables in the stock selection filter meaningfully narrowed the opportunity set…meaning, usually, not enough tickers were regularly generated [through the filter] to absorb enough capital to tilt the performance meter at most large hedge funds…as position size was very limited [1-2% maximum]. The leaders wanted the model to be the hero not just a handful of stocks. So the variables had to be reduced and optimized. Seemingly redundant indicators [for the filter] were re-tested and “tossed” and, as expected, the reduced variables increased the population set of tickers…but it also ramped the incremental volatility…which was considered very bad. In order to re-dampen the volatility capital limits on portfolio slant and sector concentration, were initiated. Sometimes market neutral but usually never more than net 30% exposure in one direction and most sectors could never comprise more than 5% of the entire portfolio. We used to joke that these portfolios were so neutered that it might be impossible for them to actually generate any meaningfully positive returns. At the time of “production” they actually did seem, at least as a model, “UN-BLOW-UP-ABLE” considering all the capital controls, counter correlations and redundancies.

As a general rule, hedge fund alphas tended to be shorter lived than long-only alphas, but everyone had portfolios risk controlled 18 ways to Sunday. Yet they all blew up in August 2007.

**Andy Lo explains August 2007**

Some time after that fateful month in August, Andrew Lo of MIT made an extensive study of the topic. A subsequent paper by Amir E. Khandani and Andrew W. Lo asked the question:

[What happened to the quants in August 2007? Evidence from factors and transactions data](http://newyorkfed.org/research/conference/2010/cb/Lo1.pdf)

. Here is the abstract:

> Using the simulated returns of long/short equity portfolios based on five valuation factors, we find evidence that the “Quant Meltdown” of August 2007 began in July and continued until the end of 2007\. We simulate a high-frequency marketmaking strategy, which exhibited significant losses during the week of August 6, 2007, but was profitable before and after, suggesting that the dislocation was due to market-wide de-leveraging and a sudden withdrawal of marketmaking risk capital starting August 8\. We identify two unwinds—one on August 1 starting at 10:45am and ending at 11:30am, and a second at the open on August 6, ending at 1:00pm—that began with stocks in the financial sector, long book-to-market, and short earnings momentum.

Earlier iterations of this research postulated a large seller coming to liquidate what amounted to a crowded trade, otherwise known as the Unwind Hypothesis. In other words, the majority of quants were in the same set of stocks despite the apparent diversity of their models:

> This hypothesis suggests that the initial losses during the second week of August 2007 were due to the forced liquidation of one or more large equity market-neutral portfolios, primarily to raise cash or reduce leverage, and the subsequent price impact of this massive and sudden unwinding caused other similarly constructed portfolios to experience losses. These losses, in turn, caused other funds to deleverage their portfolios, yielding additional price impact that led to further losses, more deleveraging, and so on. As with Long Term Capital Management (LTCM) and other fixed-income arbitrage funds in August 1998, the deadly feedback loop of coordinated forced liquidations leading to deterioration of collateral value took hold during the second week of August 2007, ultimately resulting in the collapse of a number of quantitative equity market-neutral managers, and double-digit losses for many others.

Fast forward to today. Dassault postulates a crowded long by the fast money crowd and their positions and returns have been exaggerated by leverage. What`s more, the assets are concentrated in just a few very large funds:

> What has changed though is the increased dollars managed by these funds [now $3.5T] and the concentration, of these dollars, at the twenty largest funds [top heavy for sure]. What has also considerably changed is the cost of money…aka leverage. It is just so much cheaper…and, of course, is still being liberally applied but, to reiterate, in fewer hands.

Add in a dash of excess conviction and hubris and you get a potential time bomb:

> 1\. Strong Conviction…aka Over Confidence +
> 2\. Low Volatility +
> 3\. High Levels/Low Costs of Leverage [irrespective of Dodd-Frank] +
> 4\. More Absolute Capital at Risk +
> 5\. Increased Concentration of “At Risk” Capital +
> 6\. “Doing the Same Thing”
> 
> …Adds up to a ***Combustible Market Cocktail***.

She concluded [emphasis added]:

> Still a catalyst is needed and, as always, ***the initial catalyst is liquidity [which typically results in a breakdown of historic correlations as the models begin to “knee-bend”***…and the perceived safety of hedges is cast in doubt] followed by margin calls [the ugly side of leverage…not to mention a whole recent slew of ETF’s that are plainly levered to begin with that, with the use of borrowed money, morph into “super-levered” financial instruments] and concluding with the ever ugly human panic element [in this case the complete disregard for the “black box” models even after doubling/trebling capital applied on the way down because the “black box” instructed you to]. When the “box” eventually gets “kicked to the curb”…that is when the selling ends…but not after some REAL financial pain.

**Spotting the crowded trade**

So far, we just have a "this will not end well" story, but we have no idea of what the crowded trades are and what the trigger for an unwind might be. Here is where things get more speculative (

***and comments from anyone who is closer to the situation are invited***

).

One of the crowded trades are algos that suppress market volatility, either by design or as a side-effect.

[Bloomberg](http://www.bloomberg.com/news/articles/2015-06-23/big-days-dying-off-in-u-s-stocks-with-no-2-move-since-december)

reported that 2% stock market moves have disappeared in 2015 and 

[Business Insider](http://www.businessinsider.com/historically-low-volatility-stock-market-2015-6)

reported that the market hasn't seen a 1% in eight straight weeks:

This kind of low realized vol environment has made stars of managers who run risky long-tailed strategies that pick up pennies in front of steamrollers. Consider, for example, this

[account](http://www.investmentnews.com/article/20150623/FREE/150629974/bond-fund-alternative-is-turning-heads-with-hot-performance)

about a fund which holds cash and sells put options on stocks that is being marketed as (*shudder*) a fixed-income alternative. The lack of recent downside equity market volatility has made this strategy a stellar performer and put up a return of 12.7%, triple the stock market.

In a separate 

[post](http://globalslant.com/2015/02/what-risk/)

, Dassault calculated the risk-adjusted returns of holding US equities in early 2015 and the results were extraordinary (recall that the Sharpe ratio = (return - risk free rate)/volatility):

> Recently I constructed a model that required one, three and five year Sharpe Ratios for the SP 500\. I also decided to include the Sortino Ratio. Prior to the results I hypothesized that the numbers ought to be pretty impressive given the endless equity “bull” since March 2009 but I was still curious to get the exact data. Plus, a weekly price chart of the SP 500, since 2009, visually reflects the anomaly of very limited draw-downs in the context of extremely strong returns. The calculations are as follows and as Mrs. Doubtfire once said…“Effie…Brace Yourself”.
> 
> **Sharpe Ratio**
> 1 Year = 1.37
> 3 Year = 1.86
> 5 Year =1.0
> 
> **Sortino Ratio**
> 1 Year = 2.65
> 3 Year = 3.41
> 5 Year = 1.69
> 
> Collectively, these numbers are clearly impressive but even more so in that they are calculated from a passive, long only strategy. This is a hedge fund manager’s worst nightmare as, for five years, most “hedging” has proved to be only performance degrading.
> 
> Furthermore, the Sortino Ratio data are nothing short of staggering. What they really say = Plenty of Gain with Very Little Pain.…and it really is unsustainable if only because it has become much too easy to generate positive returns with very little effort, pain or savvy.

To put these extraordinary Sharpe Ratios into context, the long-term Sharpe Ratios realized by legendary investors like Buffett, Robertson and Soros were in the 0.7 to 1.1 range. Yet a simple buy-and-hold strategy yielded 1, 3 and 5 year figures better than these investment giants!

These results are highly suggestive that equity volatility has been artificially suppressed in some fashion (no it probably isn't the Fed as QE programs had been well under way for years before volatility dived), As Captain Kirk might say, “Someone, or some

*thing*

, is suppressing market volatility to make it seem that stocks are safer than they are.“ Which brings us back to the

[Josh Brown](http://thereformedbroker.com/2015/06/21/are-quants-the-new-systemic-risk/)

comment earlier:

> There’s an interesting idea going around that asset management – specifically the metastasizing quantitative strategies run via black box are where the next big scare is due to come out of. Volatility has been so low, for so long, that winning trades have become crowded and leverage is bountiful. And the kicker – they’re all running the same playbook, loading up in the same trades.

Could the culprit for low vol be the black-box algos themselves? Another characteristic, or side-effect, of the low volatility environment is the stock market appreciated steadily without a 10% correction since 2011.

I have written about this theme many times before (see the

[Jim Paulsen study](http://ig.cdn.responsys.net/i4/responsysimages/str2/__RS_CP__/20150406_EMP.pdf)

indicating the steady market uptrend is breeding complacency and my own work at 

[Why I am bearish (what would change my mind)](http://humblestudentofthemarkets.blogspot.com/2015/05/why-i-am-bearish-and-what-would-change.html)

). But now, the steady uptrend is starting to crack.

This is the daily SPX chart. Note how the RSI indicator (top panel) has not flashed an overbought reading over 70 and oversold reading of below 30 in all of 2015\. The VIX Index (bottom panel) has been steadily declining. Both of these indicators are signs of a compressed volatility environment. On the other hand, the uptrend is starting to labor as the SPX index is losing momentum and appears to be rolling over.

The longer term 20-year monthly chart shows that the MACD histogram fell to a negative reading in January 2015, rose briefly and fell back into negative territory in March. These are the typical signs of a loss of price momentum cited in the Paulsen study. Every past instance in the last 20 years has resolved themselves in bear phases.

If these "black box algos" have been suppressing volatility either as a side-effect or by design, but they need a steadily rising stock market to make money, then could these indications that these models are starting to “knee-bend“?

We can make an educated guess. An examination of the returns of the HFRX equity market neutral hedge fund index*, which is how many of these algo strategies would be classified (though there would be other equity market-neutral strategies in that index) shows that these strategies have been struggling in 2015 with flat returns, though returns were positive in 2013 and 2014\. The evidence is tantalizing and suggestive, but not conclusive as returns were not exactly stellar in past years.

**Don`t panic on an algo unwind!**

If I am correct in my hypothesis that these algos are both suppressing equity volatility but require a steadily rising market to achieve returns, then the day of reckoning may be near.

The damage level depends on how crowded the trade is. If the trade isn't very crowded, then we may see a quick ”flash crash”, where these strategies blow up and the market returns to normal within a day or two. On the other hand, if the unwind becomes a ”margin clerk” market that requires a liquidation period of several weeks, then we may see a LTCM or 1987 style crash and snapback.

Should we encounter such market turbulence, my inner investor believes that the best thing to do is nothing. Even if we suffered the the worst case of a 1987 event, the market came back to normal within a few months. On the other hand, those who panicked and blinked got hurt very badly.

* Astute readers will ask why a market-neutral strategy requires market direction to make money. I was the analyst who initiated and wrote the BoAML Hedge Fund Monitor, in which we developed a heuristic to reverse engineer the betas of various hedge fund strategies. We found that despite the name, equity market-neutral strategies were generally not market neutral and took directional beta bets.
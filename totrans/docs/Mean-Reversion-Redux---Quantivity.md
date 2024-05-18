<!--yml
category: 未分类
date: 2024-05-18 13:50:20
-->

# Mean Reversion Redux | Quantivity

> 来源：[https://quantivity.wordpress.com/2011/07/03/mean-reversion-redux/#0001-01-01](https://quantivity.wordpress.com/2011/07/03/mean-reversion-redux/#0001-01-01)

Readers of [Momentum Redux](https://quantivity.wordpress.com/2011/06/18/momentum-redux/) requested a similar post for the mean reversion literature, recognizing the ying-yang relationship of momentum and mean reversion.

One of the most interesting wrinkles is the conceptual “apples and oranges” problem induced by trading frequency; authors use the same words, but mean different things. This subtlety, confusion, and opportunity for obfuscation arises from reversion *manifesting at many frequencies simultaneously*:

*   Intraday: market making, inter-exchange arbitrage, and various recent HFT amusement
*   Days – Months: factor convergence, whether cointegration, PCA, or more modern dimensional reduction methods (such as [manifold learning](https://quantivity.wordpress.com/2011/05/08/manifold-learning-differential-geometry-machine-learning/))
*   Months – Years: “contrarian” strategies based on accounting, FF anomalies, or behavioral models

Due to this heterogeneity, reversion manifests in many statistical guises; or, in ML speak: if you can extract a *stable time-series or cross-sectional feature*, you can probably trade it.

Reversion was first considered for price and returns, both single asset and baskets. Subsequently, higher moments of time-series reversion were considered: variance, skew, and kurtosis. Cross-sectional reversion has also been extensively studied using all sorts of fun statistics and ML; the most famous three: correlation, cointegration, and PCA.

Associated trading strategies go by *many* names depending on frequency and market participant, including: statistical arbitrage, vol arbitrage, relative value, long-short, convergence, pairs, market making, *etc*. The literature for each frequency originated, and continues to evolve, fairly distinctly given different audiences.

**Scale Invariance**

An interesting meta-question which this begs is *why reversion exhibits conceptual scale invariance, while momentum does not*. For example, observe the absence of meaningful results when googling “microstructure momentum” and “variogram momentum finance”.

This distinction pervades conceptual framing, modeling, and corresponding mathematics. A microstructure explanation seems plausible: market making is intrinsically mean-reverting, as it basically boils down to *inventory control*. This contrasts with behavioral biases driving momentum, which ample recent evidence confirms via ridiculously frequent bubbles.

This explanation further suggests potential computational bias: market making is now automated, while behavioral biases are driven by humans absorbing information at varying diffusion rates and following non-mechanical rules for switching their 401K / IRA allocations (or, similarly, long-only mutual fund portfolios). This explanation is also statistically appealing, as fairly basic mathematics can prove this combo results in nonlinear and nonstationary signals.

Recognizing this distinction, the following discussion is split into two parts: intraday and interday.

**Intraday Reversion**

Intraday mean reversion is market making of one sort or another (of varying degrees of complexity), most seeking to be flat overnight; with varying definitions of flatness, including: inventory, beta exposure, moment exposure, greek exposure, *etc*. Going back many decades, both specialists and “locals” executed non-mechanical reversion trading strategies. And, folks complain today about front-running; talk about a money printing press!

[Ed Thorp](http://edwardothorp.com) and [Richard Bookstaber](http://rick.bookstaber.com/) both recently relayed the origins of automated reversion techniques, attributing credit to Gerry Bamberger in the early 1980s while introducing [David Shaw](http://www.deshaw.com/Founder.html) and Peter Muller (Process Driven Trading, apparently now PDT Advisors?), both formerly of [Morgan Stanley](http://www.morganstanley.com/). See the [Wilmott articles](http://edwardothorp.com/id9.html) and [A Demon of our Own Design](http://en.wikipedia.org/wiki/A_Demon_Of_Our_Own_Design), respectively.

The intraday reversion literature is fairly anemic, due to the following factors (maybe more?):

*   Proprietary: hedgies guard disclosure of these techniques fairly carefully
*   Data availability: tick data is difficult to accumulate, expensive to clean, and complex to maintain at scale; not to mention, exchanges have little incentive to change this, as their business model depends upon selling data
*   Cost: intraday requires low-latency execution, and thus is not amendable to retail
*   Computational: intraday is becoming increasingly about computer engineering, due to heavy computational infrastructure (colo, networking, order books, *etc*)

Intraday is increasingly moving beyond the realms of finance and econometrics, and closer to ML and computer science / engineering, due to computational complexity (both execution and large-scale data management). While this makes it interesting for Quantivity, pure finance folks are at increasing disadvantage.

Academically, intraday is considered primarily by the market microstructure literature. See the [JFM Editorial Board](http://www.elsevier.com/wps/find/journaleditorialboard.cws_home/600652/editorialboard) for prominent researchers; arguably the three best known are [Harris](http://www-bcf.usc.edu/~lharris/), [O’Hara](http://www.johnson.cornell.edu/Faculty-And-Research/Profile.aspx?id=mo19), and [Hasbrouck](http://pages.stern.nyu.edu/~jhasbrou/). The following are representative microstructure literature:

*   [A Transaction Data Study of Weekly and Intradaily Patterns in Stock Returns](http://ideas.repec.org/a/eee/jfinec/v16y1986i1p99-117.html), Harris (1984)
*   [Estimating the components of the bid/ask spread](http://ideas.repec.org/a/eee/jfinec/v21y1988i1p123-142.html), Glosten and Harris (1985)
*   [The Microeconomics of Market Making](http://www.jstor.org/pss/2330686), O’Hara and Oldfield (1986)
*   [The Trades of Market Makers: An Empirical Analysis of NYSE Specialists](http://www.jstor.org/pss/2329060), Hasbrouck and Sofianos (1993)
*   [An Analysis of Changes in Specialist Inventories and Quotations](http://www.jstor.org/pss/2329061), Madhavan and Smidt (1993)
*   [Life in the Pits: Competitive Market Making and Inventory Control](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=7464), Manaster and Mann (1996)
*   The Statistics of Statistical Arbitrage, Fernholz and Maguire (2007)
*   [Mean reversion in short-horizon expected returns](http://www.jstor.org/pss/2962048), by Conrad and Kaul (1989)
*   [Pairs Trading: Performance of a Relative Value Arbitrage Rule](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=141615), Gatev, Goetzmann, and Rouwenhorst (1998)

As [previously reviewed](https://quantivity.wordpress.com/2010/01/12/how-to-learn-algorithmic-trading-part-3/), book-length treatments on microstructure are available in [Trading and Exchanges: Market Microstructure for Practitioners](http://books.google.com/books?id=Rd9hDRR1Yx4C) (Harris), [Empirical Market Microstructure](http://books.google.com/books?id=aaReNv846eMC) (Hasbrouck), and [Market Microstructure Theory](http://books.google.com/books?id=udXjR2Dg7bwC) (O’Hara).

**Interday Reversion**

Interday reversion has origins similar to [momentum](https://quantivity.wordpress.com/2011/06/18/momentum-redux/): long staple of technical analysis, more recently formalized by academic treatment stemming from the EMH debate. While this literature is equally massive, the following articles embody major evolution points:

*   [Does the Stock Market Overreact?](http://www.jstor.org/pss/2327804), De Bondt and Thaler (1985)
*   [Mean Reversion in Stock Prices: Evidence and Implications](http://ideas.repec.org/p/nbr/nberwo/2343.html), Poterba and Summers (1987)
*   [Common Nonstationary Components of Asset Prices](http://ideas.repec.org/a/eee/dyncon/v12y1988i2-3p347-364.html), Bossaerts (1988)
*   [When are Contrarian Profits due to Stock Market Overreaction](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=227214), Lo and MacKinlay (1990)
*   [Evidence of Predictable Behavior of Security Returns](http://ideas.repec.org/a/bla/jfinan/v45y1990i3p881-98.html), Jegadeesh (1990)
*   [Fads, Martingales, and Market Efficiency](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=227518), Lehmann (1990)
*   A Computational Methodology for Modelling the Dynamics of Statistical Arbitrage, Burgess (1999)
*   [Statistical Arbitrage in the US Equities Market](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1153505), Avellaneda and Lee (2008)

The first well-known six introduce reversion and FF overreaction anomaly, in various guises (not surprisingly, a few names are in common with the [momentum](https://quantivity.wordpress.com/2011/06/18/momentum-redux/) literature). The Burgess dissertation capstones 4 years of research on automation and use of fledging machine learning techniques for interday reversion (see references for a dozen preceding publications by Burgess). Proving the world is small, Burgess is employed by…you guessed it, Morgan Stanley. Finally, Avellaneda and Lee retrospectively survey the landscape, chronicling the competition and eventual trading flat of elementary intraday reversion strategies.

The wonderful irony of all this is it indeed confirms the existence of (not necessarily risk-free) arbitrage: money *can* be made with strategies derived from these concepts, modulo the existence of non-zero time restrictions on when such is possible (*i.e.* may not be possible today). Proof is by contradiction: if this were not true, the corresponding counterparty strategy would always succeed and thus constitute a free lunch.
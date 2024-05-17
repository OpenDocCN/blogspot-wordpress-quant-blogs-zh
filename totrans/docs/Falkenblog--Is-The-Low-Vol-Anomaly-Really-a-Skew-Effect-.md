<!--yml
category: 未分类
date: 2024-05-12 20:03:29
-->

# Falkenblog: Is The Low Vol Anomaly Really a Skew Effect?

> 来源：[http://falkenblog.blogspot.com/2013/08/is-low-vol-anomaly-really-skew-effect.html#0001-01-01](http://falkenblog.blogspot.com/2013/08/is-low-vol-anomaly-really-skew-effect.html#0001-01-01)

The idea that low volatility stocks have higher returns than high volatility stocks is difficult for economists to digest, because it's so hard to square with standard theory.  It brings to mind Dostoyevsky's line "If God is dead, then everything is permitted." Similarly, when one sees their favored theory as being abandoned, it seems like all explanation is lost and chaos reigns. Yet, when a wrong theory is adopted, well, as the ever-logical Bertrand Russel used to note, if 1+1=1, everything is both true and untrue.  We need a framework to evaluate reality, and it has to be consistent.

Alas, many frameworks are largely untrue, leading to inconsistencies and explanations that are transparently tendentious.  The sign of a bad

*Weltanschauung*

is that explanations for reality become more and more convoluted, like epicycles in Ptolemaic astronomy. I'll gladly enjoy the h

[ypocrisy](http://www.brainyquote.com/quotes/quotes/f/francoisde124518.html)

of those who don't share my worldview because, as the Detroit bankruptcy has reminded us (eg, its bankruptcy blamed on too much or too little gov't), people might admit tactical errors, but they'll go to their grave with their worldview (see

[Max Planck](http://www.realclearscience.com/2013/02/15/science_advances_one_funeral_at_a_time_251521.html)

).

Consider the recent papers arguing that low volatility is really just a skew effect, in which case their worldview is safe. In the recent J

*ournal of Economic Perspectives, *

longtime behavioral finance academic

[Nicholas Barberis](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=327880)

 wrote a

[paper](http://www.aeaweb.org/articles.php?doi=10.1257/jep.27.1.173)

on Kahneman and Tversky's

[prospect theory](http://en.wikipedia.org/wiki/Prospect_theory)

 (that's

*Nobel prize winning*

Danny Kahneman, who's unimpeachability seems somewhere around that of Nelson Mandela)  It's helpful to note that this insight is 34 years old, because many  seem to all think these newfangled behavioural insights are going to revolutionize economics as if they haven't been applied continuously over the past generation.

Barberis goes over his Barberis and Huang (2008) model where prospect theory is used to motivate the hypothesis that a security’s skewness in the distribution of its returns will be priced. A positively skewed security— a security whose return distribution has a right, upper, tail is longer than its left tail—will be overpriced relative to the price it would command in an economy with standard  investors. As a result, investors are willing to pay a high price for lottery-ticket type stocks.

Barberis references several papers, including

[Bali, Cakici, and Whitelaw (2011)](http://faculty.msb.edu/tgb27/BaliCakiciWhitelawJFE2010.pdf)

, and Conrad, Dittmar, and Ghysels (

[here's](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1522218)

the 2009 version, though a more recent version was

[just published](http://onlinelibrary.wiley.com/doi/10.1111/j.1540-6261.2012.01795.x/full)

in the

*Journal of Finance*

).  He also finds it relevant to the underperformance of IPOs, the low average return of distressed stocks, of bankrupt stocks, of stocks traded over the counter, and of out-of-the-money options (all of these assets have positively skewed returns); the low relative valuations of conglomerates as compared to single-segment firms (single-segment firms have more skewed returns); and the lack of diversification in many household portfolios (households may choose to be undiversified in positively skewed stocks so as to give themselves at least a small chance of becoming wealthy).

It seems like an orthogonal way to address these puzzles compared to the constrained rational approach offered by

[Betting Against Beta](http://pages.stern.nyu.edu/~lpederse/papers/BettingAgainstBeta.pdf)

, but there's a problem, and it's that the well-know equity risk premium has a

*negative*

skew relative to what's considered less premium-worthy, long-term bonds. That is, equities in general have a lower (ie, more negative) skew than bonds, and this is the most prominent 'risk premium', so it must not be an exception to a rule.

**US Monthly Data 1962-2013**

|  |  
> 10-year US T-Bond

 |  
> SP500 Index

 |
| AnnRet | 7.05% | 7.28% |
| AnnStdev | 6.86% | 15.05% |
| Skew | 61.09% | -42.16% |

Note that indices have negative skew while individual stocks have positive skew.  This is because correlations go up in down markets, and this predictable tendency creates a problem for idiosyncratic skew pricing models.  That is, in the CAPM and other asset pricing models, risk factors have prices that are linear in the covariances, otherwise there is arbitrage, the essence of the Arbitrage Pricing Theory: whatever risks are priced, they are based on additive moments, so risk and returns are linear functions.  Now we have priced risks that are not just diversifiable, but change sign depending on what else is in the portfolio.  If true, there is an implausible level of profit to be had from buying portfolios and selling the constituents.

As an ivy league confabulator Barberis deftly ignores this inconsistency and instead notes that the equity risk premium makes perfect sense given

[Benartzi and Thaler’s (1995)](http://www.jstor.org/discover/10.2307/2118511?uid=3739256&uid=2&uid=4&sid=21102549812767)

idea that if you focus only on the net changes in wealth (technically, U(x) vs. U(w+x)), you can get this to work in 

*cumulative *

prospect theory, because losses hurt more than gains, so one gets paid to take risk in this case.

Alas, there's a limit to how much skew and variance can both be priced in the same universe, where people love positive skew and hate variance.  If skew explains

*most*

of the volatility anomaly, that implies people can't be globally risk averse because they would like extremum up-moves too much, and these happen proportionally more for volatile stocks.  Yet if that's true there's no risk premium of any sort, because people would simply buy single assets or derivatives and have no incentive to mitigate risk via bundling and arbitrage.  This has been shown formally by

[Levy, Post, and van Vliet (2003)](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=411660)

, but it should be intuitive: skew is positively correlated with volatility for stocks with lognormal returns, so there's a point at which one's love of skew dominates one's fear of volatility. If that point is reached, volatility is always less costly than skew is beneficial. This constrains the size of the skew-loving effect to be an order of magnitude less than the risk premium if global risk aversion exists. If global risk aversion does not exist, then the rest of the general framework presented in simply meaningless.

 So we have  prospect theory explaining the overpricing of high volatility stocks due to skew, the underpricing of equity indices due to 'narrow framing.' One could add that prospect theory is used to explain why people overpay for longshots at the horse track, in that 'decisions weights' applied to payoffs prospect theory are observationally equivalent to overoptimistic probability assessments (see

[Snowberg and Wolfers](http://www.hss.caltech.edu/~snowberg/papers/Snowberg-Wolfers%20Risk%20Love%20or%20Decision%20Weights-NBER.pdf)

(2010)), and that Danny Kahneman is an admirer of Nassim Taleb's Black Swan theory, which argues that small probability events are generally underappreciated. In other words, whatever the probability density function and expected return, it's explained by prospect theory.

Skew also shows up also in the recent publication of

[Conrad, Dittmar, and Ghysels](http://www.afajof.org/details/journalArticle/4240261/Ex-Ante-Skewness-and-Expected-Stock-Returns.html)

(2013), who are incredibly meticulous in their analysis of how skew relates to future returns, highlighting what three top researchers over several years can do to data.  Yet, they then ignore the elephant in the room, that is, if volatility is negatively priced and skew is positively priced, how do these both exist in equilibrium?  It should be hard for these authors to say they don't care, because they are very exhaustive in their analysis, noting at one point:

> We use several methods to estimate [the stochastic discount function] M[t](τ) that allow for higher co-moments to influence required returns. These methods differ in the details of specific factor proxies, the number of higher co-moments allowed, and the construction of the SDF.

Alas, as usual in analysis of SDFs, there is no take-away input one can use to measure risk, no soon-to-be-indispensable tool, just a promise that this has all been vouchsafed against high-falutin theory and so '

[it's all good.](http://www.urbandictionary.com/define.php?term=it's%20all%20good)

'  Consistency is a good thing, but only in certain dimensions. One of the authors, Dittmar (2002), wrote a v

[ery nice paper](http://onlinelibrary.wiley.com/doi/10.1111/1540-6261.00425/abstract)

 for the

*Journal of Finance*

in 2002 noting that if you restricts a non-linear pricing kernel to obey the risk-aversion needed to ensure that the market portfolio is the optimal portfolio, the explanatory power goes away of higher moments. With all the abstruse checks in this paper, one would think he might want to address that issue, but instead he ignores it.

I'm sure former

*JoF*

editor

[Cam Harvey](http://people.duke.edu/~charvey/)

read this while nodding approvingly throughout (he's referenced every other page, and a big believer that risk explains most everything in finance).  While understanding SDFs and their risk premiums won't help you get a job at a hedge fund, it will help you get published and be popular among publishing academics.

I agree that skew is important, as it measures the upside potential that delusional lottery-ticket buying investors love, and because of relative wealth preferences, arbitrage is costly and their footprint remains.  That's a mathematically consistent story.  Skew loving effects can't exist on the same par with variance hating effects in any consistent story about asset returns. Is this important?  Consistency can be overdone, but I don't think this is foolish because one tends to see what one believes rather than vice versa, and I think there's more power and predictability in viewing volatility as merely a desirable attribute for delusional investors, as opposed to something that pays you a premium.

Paradoxically, behavioral refinements such as prospect theory are preventing needed outside-the-box adjustments and are used to maintain a defective status quo, one that has been wrong on a profound empirical issue for 50 years (ie, the risk premium). These putative revolutionary insights allow academics to wax eloquent on how their complex paradigm handles subtleties such as any of those 50 behavioral quirks, and outside commentators are pleased to be part of a new vanguard, obliviously marching in basically the same, pointless, confabulating path.
<!--yml
category: 未分类
date: 2024-05-18 13:54:49
-->

# Statistical Arbitrage & Optimality | Quantivity

> 来源：[https://quantivity.wordpress.com/2009/12/28/statistical-arbitrage-optimality/#0001-01-01](https://quantivity.wordpress.com/2009/12/28/statistical-arbitrage-optimality/#0001-01-01)

Readers interested in statistical arbitrage (statarb) strategies may enjoy brief review of two recent articles: [Statistical Arbitrage in the U.S. Equities Market](http://www.math.nyu.edu/faculty/avellane/AvellanedaLeeStatArb071108.pdf) by Avellaneda and Lee (15 Jun 2009 draft) and [Analytic Solutions for Optimal Statistical Arbitrage Trading](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1505073) by Bertram (12 Nov 2009 draft).

Avellaneda and Lee survey the results of statarb over 1997 – 2007, focusing on both classic approaches: co-integration (beta-neutralized sector ETFs) and [PCA](http://en.wikipedia.org/wiki/Principal_component_analysis) (factors and market-neutralized eigenportfolios). One of the better concise summaries of statarb methodology, outside the few early Ph.D. thesis published on the topic (*e.g.* Burgess). Section 6 is interesting, as it draws an equivalence between volume-weighting returns (originally popularized by technical analysis) and measuring returns in “trading time” (recently popularized by Dacorogna *et al.*); using such adjustment increases Sharpe by 37% sharpe (1.51 from 1.1, admittedly neither stellar). Given the broad applicability of both volume-weighting and “trading time” across diverse quantitative strategies, this article is worth review.

Bertram presents closed-form solutions for “optimal statistical arbitrage strategies with transaction costs”, derived from Taylor series approximation of real-valued integral. One interesting result, from § 3.1 is the assertion that *optimal entry and exit bands are symmetric around zero* (which differs from historical practice, in which such expectations were both *ad hoc* and tended to be asymmetric). Other interesting results are closed-form solutions for mean and variance of trade length and strategy return.

Bertram’s article follows the technical style, with heavy emphasis on stochastic processes, from his 2005 dissertation: [Modelling Asset Dynamics via an Empirical Investigation of Austrialian Stock Exchange Data](http://ses.library.usyd.edu.au/handle/2123/1593). Both are worth reading, albeit both being a bit formal.
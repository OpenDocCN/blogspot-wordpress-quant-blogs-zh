<!--yml
category: 未分类
date: 2024-05-18 13:56:49
-->

# Quantivity | Uncommon Returns through Quantitative and Algorithmic Trading

> 来源：[https://quantivity.wordpress.com#0001-01-01](https://quantivity.wordpress.com#0001-01-01)

An astute reader suggested reproducing the results from a recent article on regime analysis by Kritzman *et al.*, [Regime Shifts: Implications for Dynamic Strategies](http://www.cfapubs.org/doi/abs/10.2469/faj.v68.n3.3) in FAJ (May / June 2012). This is a fun exercise to be conducted over a series of posts, as doing so illustrates several important economic principles and some elegant mathematics.

This post begins by identifying *macroeconomic market regimes arising from multi-asset economic activity*.

[Read more…](https://quantivity.wordpress.com/2012/11/09/multi-asset-market-regimes/#more-10079)

Tadas asked an interesting question in his recent post: [Where did all the finance bloggers go?](http://abnormalreturns.com/where-did-all-the-finance-bloggers-go/) A variety of folks gave thoughtful replies: [Josh Brown](http://www.thereformedbroker.com/2012/10/23/where-did-all-the-finance-bloggers-go-my-theories/), [Flex Salmon](http://blogs.reuters.com/felix-salmon/2012/10/23/did-the-financial-blogosphere-go-away/), [David Merkel](http://alephblog.com/2012/10/24/why-i-love-blogging/), [Scott Bell](http://iheartwallstreet.com/2012/10/24/why-i-stopped-blogging/), the [Macro Men](http://macro-man.blogspot.com/2012/10/introspection-day.html), and bunch of [anonymous professional traders](http://www.rmdfx.com/2012/10/24/prominent-market-players-talk-about-this-market-enviroment/). Undoubtedly, there is truth in all their observations.

Yet, perhaps there is a common root cause at work, not yet stated: *implicit momentum bias*.

[Read more…](https://quantivity.wordpress.com/2012/10/25/implicit-momentum-bias/#more-9948)

GOOG unexpectedly disclosed their Q3 earnings early last week, on October 18th. While earnings were marginally interesting, much more amusing was the corresponding hiccup in intraday trading. This event provides an opportunity to dig into TAQ data, view through a HFT lens, and build intuition from some elegant ideas due to Mendelbrot, Clark, and Ané.

[Read more…](https://quantivity.wordpress.com/2012/10/23/volume-clock-gaps-and-goog/#more-9778)

Quantivity disliked undergrad [macroecon](http://en.wikipedia.org/wiki/Macroeconomics), as it was largely a waste of time: fancy theory lacking compelling evidence, amplified by no consensus within the field à la [saltwater versus freshwater](http://en.wikipedia.org/wiki/Saltwater_and_freshwater_economics).

Few folks could be blamed for such flippancy, as it was mostly harmless throughout the [great moderation](http://en.wikipedia.org/wiki/Great_Moderation). In fact, traders took apparent pride in their ignorance of macro—except the [global macro](http://en.wikipedia.org/wiki/Global_macro) guys, obviously. Then, along came a credit crisis.

With that swan, Quantivity concluded it was high time to formulate a *systematic* macro perspective: a “top down” complement to calibrate “bottom up” quant models. Quantivity brought great humility to this effort, due to both intrinsic complexity and comparatively weaker background in macro.

This post kicks off a few thoughts derived from this effort; hopefully a welcome addition alongside micro analysis. Two caveats are worth noting. First, confirmation bias is particularly dangerous with macro, and thus emphasis is placed on broadly considering diverse viewpoints. Second, these thoughts are posted with a bit of trepidation, given intense desire to avoid politics and policymaking.

[Read more…](https://quantivity.wordpress.com/2012/05/09/macro-matters-and-orthodoxy/#more-9384)

[Index Return Decomposition](https://quantivity.wordpress.com/2011/12/14/index-return-decomposition/) prompted several readers to inquire about *forecasting the signs of returns*, as implied by the ![s_t](img/3d34b6bd645c53954926164c36a40ae9.png) decomposition variable. This is an interesting topic worth review, quick survey of intuition from the literature, and some R code for exploratory analysis.

This topic is known as *direction-of-change* forecasting in the literature. Needless to say, successful prediction of the sign for future returns is quite interesting from a trading perspective. Traditionally, only univariate return series were considered; [Anatolyev (2008)](http://www.nes.ru/~sanatoly/Papers/DepRatio.pdf) is an exception, modeling two or more interrelated markets via dependence ratios. This literature tends to be a bit obtuse, due to commonly unstated stylistic assumptions regarding conditional return dynamics.

[Read more…](https://quantivity.wordpress.com/2012/01/16/sign-direction-of-change-forecasting/#more-7655)

Quantivity is fortunate to be acquainted with numerous folks who have earned consistent returns over multiple decades without significant drawdown. Although they have varying trading strategies, there is a common theme which unifies them: top-down systematic focus on the *sociology of market participants*.

This focus is *not* behavioral finance, in search of anomalies driven by cognitive biases divergent from equilibrium (although majority do that too). Rather asking inferential sociological questions, such as: was the market “efficient”, in the [Fama](http://en.wikipedia.org/wiki/Efficient-market_hypothesis) sense, during the post-war decades prior to 2000 *because people expected it to be* (blissfully ignoring a few [hiccups](http://en.wikipedia.org/wiki/Black_Monday_%281987%29)); in contrast to how it is commonly understood and formalized, with reverse causality: market is assumed to be efficient, thus people understand it as such.

Similarly, have the past 15 years been “inefficient”, in the bubble and anomaly sense, *because* cultural faith among investors in such “efficiency” was lost; or, did they lose faith because the market became inefficient? Big difference.

In other words: *is finance governed by physics, biology, or Peltzman*?

[Read more…](https://quantivity.wordpress.com/2012/01/03/physics-biology-peltzman-finance/#more-9021)

A variety of techniques exist for estimating parameters of the return decomposition model, previously introduced in [Index Return Decomposition](https://quantivity.wordpress.com/2011/12/14/index-return-decomposition/). This post considers estimation of an *independent mixture model* via maximum likelihood (MLE), a workhorse of frequentist statistics and always a nice place to begin.

Recall ![z](img/7d74f7d8fdd6545e22c6dd9de0af53b3.png) is *unobserved*, and thus the model cannot be directly estimated via MLE. Thus, need to decide how to approach estimation for this latent variable. One way is to be naive, and simply assume ![z](img/7d74f7d8fdd6545e22c6dd9de0af53b3.png) is the deterministic difference in return between stock and index (technically, this generates a [profile likelihood](http://en.wikipedia.org/wiki/Likelihood_function#Profile_likelihood) as formalized by [Severini and Wong [1992]](http://people.csail.mit.edu/~jrennie/trg/papers/severini-conditionally-92.pdf), which [Murphy and Van Der Vaart [2000]](http://www.jstor.org/pss/2669386) verify is well-behaved consistent with exact likelihood):

   ![z_t = r_t - i_t ](img/9406f569aca4e251c598dbe26d85eef1.png)

This assumption permits focus on estimating ![\alpha](img/9a53e012ad26523af8c1a6778d340c3f.png), providing insight into the *mixing behavior* of the return being decomposed: if a stock return behaves like its index, then mixing is low with small ![\alpha](img/9a53e012ad26523af8c1a6778d340c3f.png) (in the limit, ![\alpha = 0](img/52b5c00309e065e19db837bc8b91a752.png) when a stock behaves identical to its index, as no mixing is required); in contrast, the stock return behaves independent from its index on a regular basis, then mixing is high with a large ![\alpha](img/9a53e012ad26523af8c1a6778d340c3f.png).

[Read more…](https://quantivity.wordpress.com/2011/12/28/estimating-mixture-index-return-decomposition-via-maximum-likelihood/#more-8887)

[![](img/1bdad192323ce202c0e3c5a98a73c5ee.png "Red Blooded Risk")](https://quantivity.wordpress.com/wp-content/uploads/2011/12/redblood.png) Risk is *deeply* underappreciated.

Moreover, it is misunderstood—even by many who have smelled it up close personally via big trading loses on hedged positions. Aaron Brown’s most recent text, [Red-Blooded Risk](http://books.google.com/books?id=X3sGahpmkQ0C), explains why.

In doing so, it is *simultaneously brilliant and flawed*. For the former, Brown deserves credit; for the latter, the publisher presumably deserves most of the blame.

[Read more…](https://quantivity.wordpress.com/2011/12/17/risk-pragmatics/#more-8737)

Unmasking a phenomenon ![f](img/f6f5c905b764a946a65bee80b6736fe6.png) into its constituent parts ![\textbf{g}](img/dd36de08983666821bd2eac7513fb63a.png), via *functional decomposition* ![\phi](img/2091dd12efe62f5560f0e90f96ef4889.png), is one of the great beauties of mathematics:

   ![f(\textbf{x}) = \phi(g_1(\textbf{x}), g_2(\textbf{x}), \dots, g_n(\textbf{x})) ](img/937ce0003616227e8e5a15e180ae901a.png)

This technique finds surprisingly often use in quant models.

Ongoing analysis and trading based on proxy hedging, exemplified by series beginning with [Proxy / Cross Hedging](https://quantivity.wordpress.com/2011/10/02/proxy-cross-hedging/), suggests potential for an equity decomposition model based on the relationship between returns of a stock ![r_t](img/81847f8e748a72d127acffb74b21e309.png) and its corresponding index ![i_t](img/d1ba04e50950b99d9eabd6f208278285.png):

   ![r_t = s_t \left[ \alpha_t | z_t | + (1 - \alpha_t) \beta | i_t | \right] + \epsilon_t ](img/031d799b8df5320f04bc3fef04370113.png)

To explain this model, let’s build it up from intuition.

[Read more…](https://quantivity.wordpress.com/2011/12/14/index-return-decomposition/#more-8678)

Quantivity is pleasantly surprised to discover an increasing number of folks are deriving value from the [Curated Quant Research Feed](https://quantivity.wordpress.com/2011/07/28/curated-research-feed/) on [@Quantivity](http://twitter.com/quantivity). Indeed, the combo of daily curated feed with *single-source* retrospective search has become indispensable for personal research. Towards understanding why, Kedrosky provides nice explanation in his [Curation is the New Search is the New Curation](http://paul.kedrosky.com/archives/2011/01/curation_is_the.html) post earlier this year:

> Head back to curation and watch new algos emerge on top of that next-gen curation again. Think of Twitter as a new stab at curation. Curated sites will re-seed a new generation of algorithmic search sites. In short, curation is the new search.

Indeed, intent of curation here is to maintain *high signal-to-noise ratio* for a mix of preprint and classics in a *highly-specialized* literature (*i.e.* combo of retail ![\mathbb{P}](img/f2d0e071de256bbddee88d21a6582414.png) and prop ![\mathbb{Q}](img/969ce5c634b2b4963929a6476f8ccc63.png)) for which strong motivation exists elsewhere to obfuscate; and search over the stream provides ability to both rewind time and to integrate *conceptual connectivity* spanning time.

[Read more…](https://quantivity.wordpress.com/2011/11/04/update-curated-quant-research-feed/#more-8559)
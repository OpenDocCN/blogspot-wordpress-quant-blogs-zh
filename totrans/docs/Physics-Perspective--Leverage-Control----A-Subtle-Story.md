<!--yml
category: 未分类
date: 2024-05-18 07:06:12
-->

# Physics Perspective: Leverage Control -- A Subtle Story

> 来源：[http://physicsoffinance.blogspot.com/2011/07/leverage-control-subtle-story.html#0001-01-01](http://physicsoffinance.blogspot.com/2011/07/leverage-control-subtle-story.html#0001-01-01)

I

[mentioned recently](http://physicsoffinance.blogspot.com/2011/07/leverage-control-for-market-stability.html)

some work (in progress) by Stefan Thurner and colleagues exploring how leverage influences stability (price volatility) in a competitive, speculative market. Thurner spoke about this at a meeting on Tipping Points in Durham, UK. What I find most appealing about this work is that is explores this question with a model that is rich enough to exhibit many of the basic features we see in speculative markets -- competition between hedge funds and other investment firms to attract investors' funds, the use of leverage to amplify potential gains, the monitoring of leverage by banks who lend to the investment firms, occasional abrupt crashes and bankruptcies, etc.

Is it a perfect model? Of course not, there is no such thing; models are tools for thinking. But it is arguably better than anything else we currently have for running "policy experiments" to test what might happen in such a market if regulators take this or that step -- establishing tight limits to allowed leverage, for example. 

Stefan kindly sent me the slides from his talk, a few of which I'd like to mention here. As I said, this is work in progress, so these are preliminary results. They're interesting because they suggest that avoiding dangerous market instability through leverage limits comes with costs, and that our intuition isn't at all a reliable guide -- we need these kinds of models in which we can discover surprising outcomes (before we discover them in reality).

I won't give a detailed description of the model; it can be found in an early draft of the paper available

[here](http://www.google.com/url?sa=t&source=web&cd=1&ved=0CBQQFjAA&url=http%3A%2F%2Fcowles.econ.yale.edu%2FP%2Fcd%2Fd17a%2Fd1745.pdf&rct=j&q=leverage%20causes%20fat%20tails&ei=WJMyTrGsFMySswaviKTpBg&usg=AFQjCNEsxENwyaZ27EMuMPq7UfONzS08KQ&cad=rja)

. Thurner and colleagues have been working to improve the model over several years, and it now reproduces a number of realistic market behaviors quite naturally. Thurner summarized these as follows:

In other words, the hedge funds act to eliminate mis-pricings (taking volatility out of the market), and profit by doing so. Funds have to be aggressive to survive in the face of stuff competition, but suffer if they get too large. Risks shorten the lifetime of a fund. Overall, the models also reproduces the right statistical fluctuations in the market.

As I discussed in

[my earlier post in this work](http://physicsoffinance.blogspot.com/2011/07/leverage-control-for-market-stability.html)

, competition between hedge funds leads naturally to increasing leverage and drives the market to have a fat-tailed distribution of returns; it becomes subject (like real market) to large price fluctuations as a matter of course driven by its own internal dynamics (no external impacts required). In this condition, the market is highly prone to catastrophic crashes triggered by nothing by small price fluctuations linked to noise traders (unsophisticated investors buying and selling more or less at random). The figure below shows a typical example, plotting the wealth of various funds versus time, with a dramatic crash that affects all funds at once (different colors for different funds):

![](img/2a59999f631c77aecb25c105981caf79.png)

Now, a natural question is -- could these kinds of events be avoided with proper regulations? One idea would be to restrict the amount of leverage allowed with the aim of keeping the market returns in a mode Gaussian regime, i.e. eliminating fat tails. People could probably argue for decades about whether this would work or not without coming to an answer; this model makes it possible to do an experiment to find out, which is what Thurner and colleagues have done.

Two figures (below) show some of the results, and require some explanation. The different colors correspond to different possible regulatory regimes, and show how behavior changes with maximum allowed hedge fund leverage : BLUE (no other regulations), PALE GREEN (regulations akin to Basel I and II, in which banks loaning to hedge funds are restricted by capital requirements) and RED (a situation in which banks monitor hedge funds and reduce a hedge fund's allowed leverage below the maximum when the volatility in its assets grows; a kind of adaptive leverage control). 

First, consider a figure showing how how the action of hedge funds, and their use of volatility, actually benefits the market -- making it more efficient (in one sense). 

The figure shows the mean square price volatility versus allowed leverage. Increasing leverage lets the hedge funds pounce on opportunities more aggressively and wipe out mis-pricings more effectively. Die hard free market people should love this as it shows that the effect is strongest in the absence of any regulation. The regulated markets require higher leverage to get the same reduction in volatility.

But this isn't the whole story. Now consider another figure for the probability (per unit time) of a failure of one of the hedge funds:

Here the pure free market solution isn't so good, as this probability rises rapidly with increasing leverage. There is a relatively low value of leverage (around 5 in the model's units) where the market benefits of leverage have already been realized, and more leverage only leads to more failures (because it takes the market into the regime of fat-tailed returns; this can happen even if the mean square volatility remains small).

The regulated markets in this case perform marginally better -- the regulations reduce the number of failures, and the cost for this is marginally increased volatility.

A surprising outcome is that these same regulations, in the regime of very high leverage, actually do worse than no regulations at all -- they lead to higher market volatility AND more failures as well, a truly perverse regime.

All in all, then, this model offers a sobering perspective on how regulators might go about trying to avoid crashes linked to fat tails by limiting leverage. Some limitation clearly seems to be good. But too much can be bad, especially when coupled with other market regulations. You can't test out one idea in isolation, because they interact in surprising ways.

I'll probably have some further comments on this in the near future. It's a work in progress, as is my understanding of it -- and of what it means for the bigger picture.
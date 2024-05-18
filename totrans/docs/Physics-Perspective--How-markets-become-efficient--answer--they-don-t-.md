<!--yml
category: 未分类
date: 2024-05-18 07:01:10
-->

# Physics Perspective: How markets become efficient (answer: they don't)

> 来源：[http://physicsoffinance.blogspot.com/2012/02/how-markets-become-efficient-answer.html#0001-01-01](http://physicsoffinance.blogspot.com/2012/02/how-markets-become-efficient-answer.html#0001-01-01)

A staggering amount of effort has been spent -- and wasted -- exploring the idea of market efficiency. The notoriously malleable efficient markets hypothesis (EMH) claims (in its weakest form) that markets are "information efficient" -- market movements are unpredictable because smart investors keep them that way. They should quickly -- even, "instantaneously" in some statements -- pounce on any predictable pattern in the market, and by profiting will act to wipe out that pattern.

I've written too many times (

[here](http://physicsoffinance.blogspot.com/2011/05/whats-efficient-in-efficient-markets.html)

,

[here](http://physicsoffinance.blogspot.com/2011/09/of-hurricanes-and-economic-equilibrium.html)

,

[here](http://physicsoffinance.blogspot.com/2012/01/markets-increasingly-complex-dynamics.html)

, for example) about the masses of evidence against this idea. It's not that predictable patterns don't attract investors who often act in ways that tend to wipe out those patterns through arbitrage. Part of the problem is that investors often act in ways that amplify the pattern (following trends, for example). Moreover, there are fundamental limits to arbitrage -- "the markets can stay irrational longer than you can stay solvent." Still, the EMH stumbles onward like a zombie -- dead, proven incorrect and misleading, yet still taking center place in the way many people think of markets.

I found an illuminating new perspective on the matter

[in this recent paper](http://www.bis.gov.uk/assets/bispartners/foresight/docs/computer-trading/11-1225-dr6-ecological-perspective-on-future-of-computer-trading.pdf)

by Doyne Farmer and Spyros Skouras, which explore analogies between finance and ecology. This analogy is itself deeply suggestive. They note, for example, how the interactions between hedge funds can be useful viewed in ecological terms -- funds sometimes act as direct competitors (the profits of one reducing opportunities for another), and in other cases as predator and prey or as symbiotic partners. But I want to look specifically at an effort they make to give a rough estimate of the timescale over which the actions of sophisticated arbitragers might reasonably be expected to wipe out a new predictable pattern in the market. That is, if the market for whatever reason is temporarily inefficient -- showing a predictable pattern -- how quickly should it be returned to efficiency? How long is the time to relaxation that the EMH claims is "instantaneous" or close to it?

The gist of their idea is very simple. Before you can exploit a predictable pattern, you first have to identify it. If you're going to invest money trading against it, you need to be fairly sure you've identified a real pattern, not just a statistical fluke. If you're going to invest somebody else's money, you have to convince them. This takes some time. The stronger the pattern, the more it stands out and the less time it should take to be sure. Weaker signals will be hidden by more noise, and reliable identification will take longer. Looking at how much time it should take to get good statistics should give an order of magnitude of how long a pattern should persist before any smart investor can begin reliably trading against it and (perhaps) erasing it.

Here's the specific argument, expressed using the Sharpe ratio (ratio of expected return to standard deviation of a strategy exploiting the pattern):

This makes obvious intuitive sense. If S is very large, making the pattern obvious, more deterministic and easier to exploit, then the time over which it might be expected to vanish is smaller. Truly obvious patterns can be expected to vanish quickly. But if S is small, the timescale for identification and exploitation grows.

As Farmer and Skouras note, successful investment strategies often have Sharpe ratios of about S = 1, so this gives a result of about 10 years. [This is the result if one makes the analysis on an annual timescale, with the Sharpe ratio calculated on a yearly basis. If we're talking about fast algorithmic trading, then the analysis takes place on a shorter timescale.]

So, 10 years is the order of magnitude estimate -- which is a rather peculiar interpretation of the word "instantaneous." Perhaps that word should be replaced in the EMH with "very slowly," although that somewhat dampens the appeal of the idea: "The EMH asserts that sophisticated investors will very slowly identify and exploit any inefficiencies in the market, tending the erase those inefficiencies over a few decades or so." Given that new inefficiencies can be expected the arise in the mean time, you might as well call this more plausible hypothesis the PIMH: the perpetually inefficient markets hypothesis.

And their estimate, Farmer and Skouras point out, is actually optimistic:

> We should stress that this estimate is based on idealized assumptions, such as log-normal returns – heavy tails, autocorrelations, and other effects will tend to make the timescale even longer.... As a given inefficiency is exploited, it will become weaker and the Sharpe ratio of investment strategies associated with it drops. As the Sharpe ratio becomes smaller the fluctuations in its returns become bigger, which can generate uncertainty about whether or not the strategy is still viable. This slows down the approach to inefficiency even more.

Of course, as I mentioned above, this analysis depends on timescale. Take t in years and we're thinking about predictable patterns emerging on the usual investment horizon of a year or longer, patterns exploited by hedge funds and mutual funds of the more traditional (not high frequency) kind.  Here we see that the time to expect predictable patterns to be wiped out is very long indeed. If 10 years is the order of magnitude, then it's likely some of these patterns persist for several decades -- getting up to the time of a typical investing career. Hardcore supporters of the EMH should learn to speak more honestly: "We have every reason to expect that predictable market inefficiencies should be wiped out fairly quickly, at least on the timescale of a human investment career."

All in all, this way of estimating the time for relaxation back to the "efficient equilibrium" suggests that the relaxation is anything but fast, and often very slow. The EMH may be right that there likely aren't any obvious patterns, but more subtle predictable patterns will likely persist for long periods of time, even while they present real profit opportunities. The market is not in equilibrium. And with no mechanism to prevent them, new predictable patterns and "inefficiencies" should be emerging all the time.
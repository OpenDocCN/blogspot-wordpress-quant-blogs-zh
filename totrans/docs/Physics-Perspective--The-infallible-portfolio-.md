<!--yml
category: 未分类
date: 2024-05-18 06:59:43
-->

# Physics Perspective: The infallible portfolio?

> 来源：[http://physicsoffinance.blogspot.com/2012/11/the-infallible-portfolio.html#0001-01-01](http://physicsoffinance.blogspot.com/2012/11/the-infallible-portfolio.html#0001-01-01)

In

[this short essay](http://baselinescenario.com/2012/11/29/high-frequency-trading-and-high-returns/?utm_source=feedburner&utm_medium=feed&utm_campaign=Feed%3A+BaselineScenario+%28The+Baseline+Scenario%29)

, Ricardo Fenholz of Columbia University makes what seems (to me at least) to be a rather incredible claim: that it's relatively easy to construct a portfolio that is guaranteed to outperform the S&P 500 over one year (or any other interval you like) and also has a limited downside during that year. The idea is the take the S&P 500 Index and tweak it a little, creating a portfolio with less weight in stocks with higher capitalization, and more weight in those with less capitalization, and presto -- you have something guaranteed to outperform the S&P 500, he claims. Is that possible? That easy? Here's a little more detail:

> To understand how this works, let’s consider the S&P 500 U.S. stock index. Suppose that we wish to invest some money in S&P 500 stocks for one year. Currently, Apple has a total market capitalization of roughly $500 billion, making it the largest stock in the S&P 500 and equal to approximately 4% of the total capitalization of the entire index. Suppose that we believe it is very unlikely or impossible that either Apple or any other corporation’s capitalization will be equal to more than 99% of the total S&P 500 capitalization for this entire year during which we plan to invest. As long as this turns out to be true, then it is actually pretty simple to construct a portfolio containing S&P 500 stocks that is guaranteed to outperform the S&P 500 index over the course of the year and that has a limited downside relative to this index. In essence, we can construct a portfolio that will never fall below the value of the S&P 500 index by more than, say, 5% and that is guaranteed to achieve a higher value than the S&P 500 index by the end of the year.[1]

> This is not a trivial proposition. If we combine a long position in this outperforming portfolio together with a short position in the S&P 500 index, then we have a trading strategy that requires no initial investment, has a limited downside, and is guaranteed to produce positive wealth by the end of the year. According to standard financial theory, this should not be possible.[2] Furthermore, the assumptions that guarantee that our portfolio will outperform the S&P 500 index appear entirely reasonable. After all, not for one day in the more than 50-year history of the S&P 500 has one corporation’s market capitalization come anywhere close to equaling even 50% of the total capitalization of the market. A 99% share of total market capitalization would essentially amount to there being only one corporation in the entire U. S. for an entire year. This seems like neither a likely outcome nor one that investors should take seriously when constructing their portfolios.

> What does a portfolio made up of S&P 500 stocks that is guaranteed to outperform the S&P 500 index look like? There are many different ways in which such a portfolio can be constructed, but one feature common to all such portfolios is that relative to the S&P 500 index itself, they place more weight on those stocks with small total market capitalizations and less weight on those stocks with large total market capitalizations. The weight that an index such as the S&P 500 places on each individual stock is equal to the ratio of that stock’s total market capitalization relative to all stocks’ total market capitalizations taken together. In the case of Apple, then, the S&P 500 index would place a weight of roughly 4% in this individual stock while those portfolios that use HFT to outperform this index would instead place a weight of less than 4% in Apple stock.

The only condition for this to work, he suggests, is that the assumption that no stock in the market comes to dominate the market in the sense that its market capitalization comes to be a high fraction of that of the entire market. This is, as he notes, a fairly weak assumption, although the weaker you make the assumption, the longer the time interval over which this idea apparently works.

Now, I'm not doubting the veracity of this claim. I'm just stunned that such a simple recipe could work, and can't see the intuition behind it. What if the high cap stocks happen to perform brilliantly next year, relative to the lower cap stocks? Wouldn't this portfolio with underweighted high cap stocks then underperform the S&P Index? I've had a quick look at

[the paper](http://www.math.columbia.edu/~ik/FKK.pdf)

Fernholz references as a detailed support of his claim, and there he explains the conditions for the theorem to hold in slightly different terms:

> The conditions mandate, roughly, that the largest stock have "strongly negative" rate of growth, resulting in a sufficiently strong repelling drift away from an appropriate boundary; and that all other stocks have "sufficiently high" rates of growth.

That sounds very different from the quite plausible assumption about no market dominance of a single stock. Indeed, this seems like saying that, if one assumes that large cap stocks will perform poorly, and small caps stock better, then we can build a portfolio guaranteed to outperform the S&P 500 Index by weighting small cap stocks more heavily. Isn't that like assuming we know the future?

But maybe I'm wrong. I'd be interested in the thoughts of others. The paper is quite dense and light on intuitive discussion of the logic. Fernholz suggests that perhaps the existence of these superior portfolios -- which require continuous rebalancing by high-frequency buying and selling of many stocks -- explains some of the very high profits consistently earned by quantitative high-frequency hedge funds such as Renaissance Technology's Medallion Fund. I think I find more convincing

[the analysis of Lo and Khandani](http://web.mit.edu/alo/www/Papers/august07.pdf)

which seemed to suggest that much of the performance of quant hedge funds over the past decade or so can be accounted for by fairly vanilla long short equity strategies, with increasing use of leverage in the mid 2000s (used to maintain high reported earnings even as raw earnings fell off due to competition).
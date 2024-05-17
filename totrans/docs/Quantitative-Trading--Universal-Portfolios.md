<!--yml
category: 未分类
date: 2024-05-12 19:25:49
-->

# Quantitative Trading: Universal Portfolios

> 来源：[http://epchan.blogspot.com/2007/01/universal-portfolios.html#0001-01-01](http://epchan.blogspot.com/2007/01/universal-portfolios.html#0001-01-01)

Let me describe a portfolio optimization scheme that, over the long run, is supposedly guaranteed to outperform the best stock in the portfolio.

Before we begin, let’s agree that we will rebalance our portfolio every day so that each stock has a fixed percent allocation of capital, just as your favorite financial consultant would have advised you. What this means is that if you own IBM and MSFT, and IBM went up after one day whereas MSFT went down, you should sell some IBM and use the capital to buy some more MSFT. There is a technical term for such portfolios: they are called “constant rebalanced portfolios”. Notice also the similarity with the Kelly criterion which I

[wrote about](http://epchan.blogspot.com/2006/10/how-much-leverage-should-you-use.html)

before: Kelly criterion asks you to maintain a constant leverage, which is like maintaining a fixed percent allocation between cash (debt) and stock.

But what should the fixed percent allocation be? Here is where the scheme gets interesting. Suppose we start with an equal capital allocation, for lack of any better choice. At the end of the day, your portfolio has a certain net worth. But then you can calculate what the net worth would have turned out if you had started with a different allocation. Indeed, we can run this simulation: try all possible initial allocations, and calculate the hypothetical net worth of the resulting portfolio. Use these hypothetical net worth as weights (after normalizing them by the sum of all net worth), and compute a weighted-average percent allocation. Finally, adopt this weighted average allocation as the new desired allocation and rebalance the portfolio accordingly. So actually the “fixed” percent allocation is not fixed after-all: it gets adjusted daily, but probably not by much. Repeat this process everyday, always calculating a new weighted allocation by simulating various initial allocations since day 1.

This scheme of portfolio optimization can be proven to produce a net worth greater than just holding the best stock, given long enough time. If this sounds like a miracle, it is partly because this is in fact an ingenious result of information theory, and partly because there are various caveats that actually limit its practical application. The proof that it works (at least in theory) is rather technical and I will let the interested reader peruse the original

[paper](http://itg.stanford.edu/~cover/papers/universal_portfolios.pdf)

published by Prof. Thomas Cover, a noted information theorist from Stanford University. He coined the term “Universal Portfolios” for portfolios rebalanced/optimized with this scheme. Without understanding the mathematical intuition, this scheme may appeal to those who believe in long-term trending behavior of stocks, because if a stock performs very well in the past, we will end up allocating more capital to it in the long run. It may also appeal to those who believe in short-term mean reversal behavior, since in the short-term, we are performing daily rebalancing of the stock positions based on an approximately constant allocation. However, this seeming confirmation of either trending or mean-reverting characteristics of stock prices is illusory – this scheme is supposed to work even if the stock prices are totally random! How can we manage to squeeze out a gain even with random price series? Remember that we have done the opposite before (see my earlier

[articles](http://epchan.blogspot.com/2006/11/correction-maximizing-compounded-rate.html)

): we manage to lose money even when a price series exhibits a geometric random walk. So it is not too surprising that we can also make money using similar information theoretic juggling.

Now for the caveats. Every time an information theorist start saying “In the long run, …”, you will be well-advised to ask: How long? In my geometric random walk

[example](http://epchan.blogspot.com/2006/11/correction-maximizing-compounded-rate.html)

where the volatility (standard deviation) of returns every period is 1%, we find that the compounded rate of return is an agonizingly small -0.005% per period. In the case of the universal portfolio scheme, the out-performance over the best stock in the portfolio is similarly dependent on the volatilities of the stocks: the higher the volatility, the faster the out-performance. Let me run a simulation with a portfolio consisting of two ETF’s RTH and OIH. If we were to run the Universal Portfolio scheme from 2001/5/17 – 2006/12/29, I find that the cumulative return is 32% (without transaction cost). Contrast that with just buying-and-holding the best ETF (namely OIH here): the cumulative return is 54%. The Universal Portfolio loses. Does this mean the theory is wrong? Not really: RTH and OIH may just have too low volatility. Herein lies the first practical caveat with the Universal Portfolio scheme: it can take too long to realize its benefit if the volatility is low.

How do we find ETF’s that have high enough volatility to realize the out-performance of Universal Portfolio? Actually, we can simply boost the volatility of RTH and OIH artificially by increasing their leverage. So let’s say we leverage both of them 2x. This means their daily returns and volatilities are both doubled. Now the best ETF (which is still OIH here) has a return of 23% (why is it lower than the un-leveraged case? Remember the formula m-s2/2 in my previous

[article](http://epchan.blogspot.com/2006/11/correction-maximizing-compounded-rate.html)

.) , but the Universal Portfolio has a return of 45%. So now the Universal Portfolio wins. But this is a Pyrrhic victory: if you factor in a transaction cost of 10 basis points, the Universal Portfolio scheme actually returns only 4%. This is the second caveat of Universal Portfolios: because of the frequent rebalancing required, transaction costs tend to eat up all the out-performance.

Now there is a final caveat. The reader may ask why I don’t just pick two stocks instead of two ETF’s to illustrate this scheme. Aren’t most stocks more volatile than ETF’s and therefore much better suited for this scheme? Indeed, most academic papers, including Prof. Cover’s original paper, use a pair of stocks for illustration. But if we do that, we run the risk of introducing survivorship bias. Naturally, if you know ahead of time that none of these two stocks will go bankrupt, the Universal Portfolio scheme may look great. But if you run a simulation where one of the stocks suddenly went bankrupt one day (which tend to be a fairly mathematically discontinuous affair), the Universal Portfolio scheme will most likely not beat holding just the non-bankrupt stock in the beginning. Using ETF’s eliminated this problem. But then ETF’s are far less volatile.

So given all these caveats, is Universal Portfolio really practical? Prof. Cover seems to think so. That’s why he has started a hedge fund to prove it.
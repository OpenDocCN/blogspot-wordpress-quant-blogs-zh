<!--yml
category: 未分类
date: 2024-05-18 14:04:51
-->

# Volatility Autocorrelation in Different Markets – Quantum Financier

> 来源：[https://quantumfinancier.wordpress.com/2010/05/27/volatility-autocorrelation-in-different-markets/#0001-01-01](https://quantumfinancier.wordpress.com/2010/05/27/volatility-autocorrelation-in-different-markets/#0001-01-01)

For an introduction to autocorrelation see this previous post: [First Order Autocorrelation as a Moderator of Daily MR](https://quantumfinancier.wordpress.com/2010/05/07/first-order-autocorrelation-as-a-moderator-of-daily-mr/).

In the previous post, I looked at how autocorrelation indicated MR performance, in this post, I observed the autocorrelation of another moderator of daily follow-through; volatility. Intuitively, it makes sense for volatility to be highly autocorrelated. VIX spikes are a good example of it. Let’s look at how the autocorrelation of volatility behave during bull/bear markets as defined by the 200/50 days moving averages crossover.

For this test, I looked at the first through fifth order autocorrelation of the 21 day rolling standard deviation of SPY returns, dividing them into percentiles (using the percent rank function with a 252 days lookback period) and looked at the average and the standard deviation of the percentiles.

As I thought before beginning the test, the volatility of returns is highly autocorrelated. However I thought that a bigger difference would exist between bull and bear markets. One thing to notice in the table below is that the autocorrelation is on average greater when the 50 day MA is greater than 200 day MA for all orders. The same observation holds true regarding the standard deviation.

[![](img/b423edf8ed7aa2fbbbd6f01e1db2e899.png "Volatility Autocorrelation in Different Markets - results")](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/volatility-autocorrelation-in-different-markets-results.png)

Trading wise, this information a no direct value by itself, however it puts in numbers a well defined market mechanics. We know that volatility is easier to predict than returns, and the level of autocorrelation is greatly responsible for this fact. We also know that daily mean-reversion strategies perform better during high volatility regimes. Thus we can use the volatility autocorrelation as an indicator of the suitability of our strategy. For example, during a high volatility regime with high autocorrelation we can expect our strategy to perform well and vice-versa if we change the contingency. For a very interesting read about the predictability of volatility and its application to trading, I recommend this recent article winning the NAAIM 2010 Wagner award from Tony Cooper. [http://naaim.org/files/2010/1st_Place_Tony_Cooper_abstract.pdf](http://naaim.org/files/2010/1st_Place_Tony_Cooper_abstract.pdf)

QF
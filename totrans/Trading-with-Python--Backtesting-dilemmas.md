<!--yml
category: 未分类
date: 2024-05-18 15:42:23
-->

# Trading with Python: Backtesting dilemmas

> 来源：[http://tradingwithpython.blogspot.com/2014/05/backtesting-dilemmas.html#0001-01-01](http://tradingwithpython.blogspot.com/2014/05/backtesting-dilemmas.html#0001-01-01)

A quantitative trader faces quite some challenges on a way to a successful trading strategy. Here I’ll discuss a couple dilemmas involved in backtesting. A good trading simulation must :

1.  Be good approximation of the real world. This one is of course the most important requirement .
2.  Allow unlimited flexibility: the tooling should not stand in the way of testing out-of-the-box ideas. Everything that can be quantified should be usable.
3.  Be easy to implement & maintain. It is all about productivity and being able to test many ideas to find one that works.
4.  Allow for parameter scans, walk-forward testing and optimisations. This is needed for investigating strategy performance and stability depending on strategy parameters.

The problem with satisfying all of the requirements above is that #2 and #3 are conflicting ones. There is no tool that can do everything without the cost of high complexity (=low maintainablity). Typically, a third party point-and-click tool will severely limit freedom to test with custom signals and odd portfolios, while at the other end of the spectrum a custom-coded diy solution will require tens or more hours to implement with high chances of ending up with cluttered and unreadable code. So in attempt to combine the best of both worlds, let’s start somewehere in the middle: use an existing backtesting framework and adapt it to our taste.

In the following posts I’ll be looking at three possible candidates I’ve found:

*   [Zipline](https://github.com/quantopian/zipline) is widely known and is the engine behind Quantopian
*   [PyAlgotrade](http://gbeced.github.io/pyalgotrade/) seems to be actively developed and well-documented
*   [pybacktest](https://github.com/ematvey/pybacktest) is a light-weight vector-based framework with that might be interesting because of its simplicity and performance.

I’ll be looking at suitability of these tools benchmarking them against a hypothetical trading strategy. If none of these options fits my requirements I will have to decide if I want to invest into writing my own framework (at least by looking at the available options I’ll know what does

*not*

work) or stick with custom code for each strategy.

First one for the evaluation is

**Zipline**

.

My first impression of Zipline and

[Quantopian](https://www.quantopian.com/)

is a positive one. Zipline is backed by a team of developers and is tested in production, so quality (bugs) should be great. There is good documentation on the

[site](https://www.quantopian.com/help#api-doco)

and an example

[notebook on github](http://nbviewer.ipython.org/github/twiecki/financial-analysis-python-tutorial/blob/master/3.%20Backtesting%20using%20Zipline.ipynb)

.

To get a hang of it, I downloaded the exampe notebook and started playing with it. To my disappointment I quickly run into trouble at the first example

*Simplest Zipline Algorithm: Buy Apple*

. The dataset has only 3028 days, but running this example just took forever. Here is what I measured:

```
dma = DualMovingAverage()
%timeit perf = dma.run(data)

1 loops, best of 3: 52.5 s per loop

```

I did not expect stellar performance as zipline is an event-based backtester, but almost a minute for 3000 samples is just too bad. This kind of performance would be prohibitive for any kind of scan or optimization. Another problem would arise when working with larger datasets like intraday data or multiple securities, which can easily contain hundreds of thousands of samples.

Unfortunately, I will have to drop Zipline from the list of useable backtesters as it does not meet my requirement #4 by a fat margin.

In the following post I will be looking at PyAlgotrade.

*Note: My current system is a couple of years old, running an AMD Athlon II X2 @2800MHZ with 3GB of RAM. With vector-based backtesting I’m used to calculation times of less than a second for a single backtest and a minute or two for a parameter scan. A basic walk-forward test with 10 steps and a parameter scan for 20x20 grid would result in a whooping 66 hours with zipline. I’m not that paitient.*
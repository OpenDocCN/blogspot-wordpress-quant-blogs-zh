<!--yml
category: 未分类
date: 2024-05-18 15:42:18
-->

# Trading with Python: Backtesting dilemmas: pyalgotrade review

> 来源：[http://tradingwithpython.blogspot.com/2014/05/backtesting-dilemmas-pyalgotrade-review.html#0001-01-01](http://tradingwithpython.blogspot.com/2014/05/backtesting-dilemmas-pyalgotrade-review.html#0001-01-01)

Ok, moving on to the next contestant: [**PyAlgoTrade**](http://gbeced.github.io/pyalgotrade/)

First impression: actively developed, pretty good documentation, more than enough feautures ( TA indicators, optimizers etc) . Looks good, so I went on with the installation which also went smoothly.

The tutorial seems to be a little bit out of date, as the first command `yahoofinance.get_daily_csv()` throws an error about unknown function. No worries, the documentation is up to date and I find that the missing function is now renamed to `yahoofinance.download_daily_bars(symbol,year,csvFile)`. The problem is that this function only downloads data for *one* year instead of everything from that year to current date. So pretty useless.
After I downloaded the data myself and saved it to csv, I needed to adjust the column names because apparently pyalgotrade expects `Date,Adj Close,Close,High,Low,Open,Volume` to be in the header. That is all minor trouble.

Following through to performance testing on an SMA strategy that is provided in the tutorial. My dataset consists of 5370 days of SPY:

```
%timeit myStrategy.run()
1 loops, best of 3: 1.2 s per loop

```

That is actually pretty good for an event-based framework.

But then I tried searching documentation for functionality needed to backtest spreads and multiple asset portfolios and just could not find any. Then I tried to find a way to feed pandas DataFrame as an input to a strategy and it happens to be [not possible](https://github.com/gbeced/pyalgotrade/issues/4), which is again a big disappointment. I did not state it as a requirement in the previous post, but now I come to realisation that [pandas](http://pandas.pydata.org/) support is a must for any framework that works with time series data. Pandas was a reason for me to switch from Matlab to Python and I never want to go back.

**Conclusion** pyalgotrade does not meet my requrement for flexibility. It looks like it was designed with classic TA in mind and single instrument trading. I don’t see it as a good tool for backtesting strategies that involve multiple assets, hedging etc.
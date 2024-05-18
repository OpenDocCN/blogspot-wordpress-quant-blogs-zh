<!--yml
category: 未分类
date: 2024-05-18 15:42:10
-->

# Trading with Python: Simple backtesting module

> 来源：[http://tradingwithpython.blogspot.com/2014/07/simple-backtesting-module.html#0001-01-01](http://tradingwithpython.blogspot.com/2014/07/simple-backtesting-module.html#0001-01-01)

My search of an ideal backtesting tool (my definition of 'ideal' is described in the earlier 'Backtesting dilemmas' posts) did not result in something that I could use right away. However, reviewing the available options helped me to understand better what I really want. Of the options I've looked at,

[pybacktest](https://github.com/ematvey/pybacktest)

 was the one I liked most because of its simplicity and speed. After going through the source code,  I've got some ideas to make it simpler and a bit more elegant. From there, it was only a small step to writing my own backtester, which is now available in the

[TradingWithPython library](http://www.tradingwithpython.com/?page_id=504)

.

I have chosen an approach where the backtester contains functionality which all trading strategies share and that often gets copy-pasted. Things like calculating positions and pnl, performance metrics and making plots.

Strategy specific functionality, like determining entry and exit points should be done outside of the backtester. A typical workflow would be:

*find entry and exits -> calculate pnl and make plots with backtester -> post-process strategy data*

At this moment the module is very minimal (take a look at the source

[here](https://code.google.com/p/trading-with-python/source/browse/trunk/lib/backtest.py)

), but in the future I plan on adding profit and stop-loss exits and multi-asset portfolios.

Usage of the backtesting module is shown in this 

[**example notebook**](http://nbviewer.ipython.org/urls/dl.dropboxusercontent.com/u/11352905/notebooks/twp_302b_backtesting.ipynb)
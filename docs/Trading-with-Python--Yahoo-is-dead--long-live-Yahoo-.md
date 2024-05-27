<!--yml

分类：未分类

日期：2024-05-18 15:41:53

-->

# 用 Python 交易：雅虎已死， Yahoo 长存！

> 来源：[`tradingwithpython.blogspot.com/2017/05/yahoo-is-dead-long-live-yahoo.html#0001-01-01`](http://tradingwithpython.blogspot.com/2017/05/yahoo-is-dead-long-live-yahoo.html#0001-01-01)

2017 年 5 月 18 日，雅虎财经的 ichart 数据 API 突然关闭，没有任何通知。而且看起来它不会再回来。这使得很多人（包括我）的代码无法运行，没有合适的免费日终数据来源。现在需要采取措施。

显然，雅虎不想让我们自动下载免费数据，但手动下载仍然可行，只需点击网页上的'下载'按钮即可。

[股票代码网页](https://uk.finance.yahoo.com/quote/SPY/history?p=SPY)

通过使用一个

*cookie-crub*

虽然配对有点困难，但幸运的是仍然可行。

我现在正在更新

*tradingWithPython.yahooFinance*

库作为一个部分，我创建了一个原型脚本来展示如何获取数据。由于现在很多人都在努力让他们的代码运行，我尽快分享这个。

[笔记本可以在 Github 上找到，](https://github.com/sjev/trading-with-python/blob/master/scratch/get_yahoo_data.ipynb)

享受！

**更新：** [yahooFinance.py](https://github.com/sjev/trading-with-python/blob/fix_yahoo/lib/yahooFinance.py)

已经修复！

*注：*

提供的数据似乎已经调整了分股因素，但没有调整分红因素。

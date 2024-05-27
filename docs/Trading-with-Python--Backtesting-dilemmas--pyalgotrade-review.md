<!--yml

类别：未分类

日期：2024-05-18 15:42:18

-->

# 用 Python 交易：回测困境：pyalgotrade 评测

> 来源：[`tradingwithpython.blogspot.com/2014/05/backtesting-dilemmas-pyalgotrade-review.html#0001-01-01`](http://tradingwithpython.blogspot.com/2014/05/backtesting-dilemmas-pyalgotrade-review.html#0001-01-01)

好的，接下来看看下一个参与者：[**PyAlgoTrade**](http://gbeced.github.io/pyalgotrade/)

初印象：积极开发中，文档很不错，功能足够丰富（包括 TA 指标、优化器等）。看起来很好，所以我继续了安装过程，过程也相当顺利。

教程似乎有点过时，因为第一个命令`yahoofinance.get_daily_csv()`抛出了一个关于未知函数的错误。不用担心，文档是更新的，我发现缺失的函数现在已重命名为`yahoofinance.download_daily_bars(symbol,year,csvFile)`。问题是这个函数只下载了*一年*的数据，而不是从那一年到当前日期的所有数据。所以这个功能相当无用。

在我将数据自己下载并保存为 csv 之后，我需要调整列名，因为显然 pyalgotrade 期望`Date,Adj Close,Close,High,Low,Open,Volume`在头部。这些都是小问题。

接着，我按照教程中提供的 SMA 策略进行了性能测试。我的数据集包含了 5370 天的 SPY 数据：

```
%timeit myStrategy.run()
1 loops, best of 3: 1.2 s per loop

```

这对于一个基于事件的框架来说实际上已经相当不错了。

但是后来我尝试搜索有关回测价差和多资产组合功能的文档，却怎么也找不到。然后我尝试找到一种方法，将 pandas DataFrame 作为策略的输入，结果发现[不可能](https://github.com/gbeced/pyalgotrade/issues/4)，这又是一个大大的失望。我之前在帖子中没有把它作为一个要求提出来，但现在我意识到[pandas](http://pandas.pydata.org/)支持对于任何处理时间序列数据的框架来说是必不可少的。pandas 是我从 Matlab 转向 Python 的原因，我绝不想再回去。

**结论** pyalgotrade 不符合我对灵活性的要求。它看起来是为经典技术分析（TA）和单一乐器交易而设计的。我认为它不是一个好的多资产回测策略、对冲等工具。

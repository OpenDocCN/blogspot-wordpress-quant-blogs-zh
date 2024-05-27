<!--yml

分类：未分类

日期：2024-05-18 15:42:10

-->

# 使用 Python 进行交易：简单的回测模块

> 来源：[`tradingwithpython.blogspot.com/2014/07/simple-backtesting-module.html#0001-01-01`](http://tradingwithpython.blogspot.com/2014/07/simple-backtesting-module.html#0001-01-01)

我对理想回测工具的搜索（我之前在“回测困境”文章中描述了“理想”的定义）并没有立即找到我可以使用的工具。然而，回顾现有的选项帮助我更好地了解我真正想要什么。在我查看的选项中，

[pybacktest](https://github.com/ematvey/pybacktest)

是我最喜欢的一个，因为其简单和快速。查看源代码后，我有一些让它更简单和更优雅的想法。从那里，只需一小步就可以编写出我自己的回测器，现在它可以在

[TradingWithPython 库](http://www.tradingwithpython.com/?page_id=504)

.

我选择了一种方法，其中回测器包含所有交易策略共享的功能，这些功能通常会被复制粘贴。比如计算持仓和盈亏、绩效指标和绘制图表。

策略特定的功能，如确定买卖点应该在回测器外部完成。典型的流程如下：

*寻找买卖点 -> 使用回测器计算盈亏并绘制图表 -> 后期处理策略数据*

目前该模块非常基础（查看源代码）

[在此处](https://code.google.com/p/trading-with-python/source/browse/trunk/lib/backtest.py)

），但未来我计划添加利润和止损退出以及多资产组合。

回测模块的使用方法在本页面展示

[**示例笔记本**](http://nbviewer.ipython.org/urls/dl.dropboxusercontent.com/u/11352905/notebooks/twp_302b_backtesting.ipynb)

<!--yml

分类：未分类

日期：2024-05-18 15:43:08

-->

# 使用 Python 交易：使用 guiqwt 绘图

> 来源：[`tradingwithpython.blogspot.com/2011/12/plotting-with-guiqwt.html#0001-01-01`](http://tradingwithpython.blogspot.com/2011/12/plotting-with-guiqwt.html#0001-01-01)

虽然博客上很安静，但幕后我一直在忙于构建一个交互式 spread 扫描器。要制作一个，需要一份配料清单：

GUI 工具包：pyqt - 检查。

数据采集：ibpy & tradingWithPython.lib.yahooData - 检查。

数据容器：pandas & sqlite - 检查。

绘图库：matplotlib - 嗯... 不。

在用 pyqt 玩了几天 matplotlib 后，我必须承认它在交互式应用中的使用远非最佳。速度慢，难以集成，且交互性差。PyQwt 证明稍微好一点，但它有自己的怪癖，对我来说有点太底层了。

但正如 Python 经常发生的那样，有人，在某个地方已经写了一个非常棒的工具包，非常适合这个工作。而且看起来像

[guiqwt](http://packages.python.org/guiqwt/index.html)

就是这样。交互式图表现在只需几行代码就能实现，看看这里的示例：

[创建曲线对话框](http://code.google.com/p/trading-with-python/source/browse/trunk/cookbook/guiqwt_CurveDialog.py)

为实现此功能，我使用了 guiqwt 的示例代码并进行了一些小调整。

当然，还有结果的漂亮图片：

...如果我知道如何在 x 轴上设置日期就好了....

<!--yml

category: 未分类

date: 2024-05-18 15:19:09

-->

# 及时投资组合：债券市场如同赌场游戏 第一部分

> 来源：[`timelyportfolio.blogspot.com/2011/04/bond-market-as-casino-game-part-1.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/04/bond-market-as-casino-game-part-1.html#0001-01-01)

在这篇文章中，我正在做一件我尽量避免做的事情，尤其是在与我的客户沟通时，那就是模糊了投资与赌博之间的界限。但在阅读了 [Reuven Brenner 的](http://www.amazon.com/gp/product/0521711576/ref=as_li_qf_sp_asin_il_tl?ie=UTF8&tag=timelyp-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=0521711576) 所有著作并完成 [Ralph Vince 的 *Leverage Space Trading Model*](http://www.amazon.com/gp/product/0470455950/ref=as_li_qf_sp_asin_il_tl?ie=UTF8&tag=timelyp-20&linkCode=as2&camp=1789&creative=9325&creativeASIN=0470455950) 之后，我认为模糊界限可以提供传统方法以外的额外见解和方法。

作为一个起点，让我们在最广泛使用的债券指数巴克莱综合总回报上应用基本的概率方法，以测试我的信念，即自 1980 年以来的债券牛市为市场历史上任何投资者提供了最好的游戏之一（请参阅我在 [“债券下跌，问题开始被问出”](http://timelyportfolio.blogspot.com/2010/12/bonds-tumble-and-questions-start.html) 的文章）。在下面显示的 Microsoft Excel 数据透视表中，自 1980 年以来，巴克莱综合指数已经上涨了所有月份的 70%，上涨的月份平均回报为 1.44%，而下跌的月份为 -1.02%。如果我们把这个说成赌场术语，就像是在每 10 场游戏中赢得 7 场，并且赔率为 1.4：1。

![](https://picasaweb.google.com/lh/photo/jTUjP4OxizVAh7mdo5-48Q?feat=embedwebsite)

再来看一下，让我们使用 R 和 PerformanceAnalytics 查看直方图和箱线图。

| ![](https://picasaweb.google.com/lh/photo/jadWQXvunFo1MoJVjc0WQA?feat=embedwebsite) |
| --- |
| 来自 [TimelyPortfolio](https://picasaweb.google.com/kentonlrussell/TimelyPortfolio02?feat=embedwebsite) |

*来源：巴克莱资本，感谢 R 和 PerformanceAnalytics 的优秀贡献者*

现在我们已经确立了基本的概率，我们可以在后续的文章中利用杠杆空间技术和蒙特卡洛模拟进行各种有趣的尝试。

R 代码:

require(PerformanceAnalytics)

require(quantstrat)

#加载日期和总回报值给出的指数数据

BarAgg<-as.xts(read.csv("lbustruu.csv",row.names=1))

#转换为 PerformanceAnalytics 的月度回报系列

#使用离散 ROC 获取简单的月度回报

#((本月价值-上月价值)/上月价值)-1

BarAggReturn<-ROC(BarAgg,n=1,"discrete")

par(mfrow=c(2,1)) #2 行 1 列

chart.Histogram(BarAggReturn["1980::"],main="自 1980 年以来巴克莱综合总回报月度 % 直方图",cex.main=1,xlab=NULL,breaks=15,methods="add.centered")

图表.箱线图(BarAggReturn["1980::"],主标题="自 1980 年以来巴克莱综合回报月度百分比箱线图",主标题字体大小=1,x 轴标签=NULL,名称=FALSE)

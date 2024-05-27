<!--yml

分类：未分类

日期：2024-05-18 15:09:52

-->

# 及时投资组合：网格探索债券

> 来源：[`timelyportfolio.blogspot.com/2011/12/lattice-explore-bonds.html#0001-01-01`](http://timelyportfolio.blogspot.com/2011/12/lattice-explore-bonds.html#0001-01-01)

由于我的第五受欢迎的博文是[债券市场如赌场游戏第一部分](http://timelyportfolio.blogspot.com/2011/04/bond-market-as-casino-game-part-1.html)，我想使用先锋美国债券市场共同基金（VBMFX）的月回报来建立 lattice R 包的技能，并帮助可视化美国债券的不可思议的运行(过去 20 年的 Calmar 比率 1.37)。

虽然我主要使用 R 基础绘图、PerformanceAnalytics 图表和 ggplot，但 lattice 包提供了一组非常强大的图表工具。

我们可以从整个月的回报集的基本 QQ 图开始。

然后，我们可以按年份进行分组。

或者，我们也可以非常容易地将每个年份分成自己的面板。

这里有一个带有密度图的不同视图。

现在让我们来构建箱形图和点状图。

在整个周期的箱形图上添加一个年度点状图。

或者我们可以为每个年份添加一个箱形图。

有关我对债券的所有博文，请参见[`timelyportfolio.blogspot.com/search/label/bonds`](http://timelyportfolio.blogspot.com/search/label/bonds "http://timelyportfolio.blogspot.com/search/label/bonds")。

[R 代码来自 GIST:](https://gist.github.com/1487949)

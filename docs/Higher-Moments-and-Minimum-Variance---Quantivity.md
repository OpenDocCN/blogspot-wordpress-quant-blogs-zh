<!--yml

分类：未分类

日期：2024 年 05 月 18 日 13:51:58

-->

# 高阶矩和最小方差 | 量化投资

> 来源：[`quantivity.wordpress.com/2011/04/30/higher-moments-minimum-variance-portfolios/#0001-01-01`](https://quantivity.wordpress.com/2011/04/30/higher-moments-minimum-variance-portfolios/#0001-01-01)

之后的几篇文章将分析高阶和混合[矩](http://en.wikipedia.org/wiki/Moment_(mathematics))与[最小方差组合](https://quantivity.wordpress.com/2011/04/17/minimum-variance-portfolios/)（以及[CVaR / ES](http://en.wikipedia.org/wiki/Expected_shortfall)和[低阶矩](http://en.wikipedia.org/wiki/Moment_(mathematics)#Partial_moments))的相关性和比较表现，延伸之前的[美国部门](https://quantivity.wordpress.com/2011/04/22/minimum-variance-sector-rotation-part-2/)和[全球轮换](https://quantivity.wordpress.com/2011/04/24/minimum-variance-global-rotation/)模型。为了激励这一点，考虑来自[Amaya and Vasquez](http://www.efmaefm.org/0EFMAMEETINGS/EFMA%20ANNUAL%20MEETINGS/2010-Aarhus/EFMA2010_0137_fullpaper.pdf) [2010]的以下引用，其中推测*波动率的补偿取决于偏度水平*（第 16 页）：

> 具有负偏度的股票得到的补偿与平均波动模型所建议的一样：更多的波动会转化为更多的回报。然而，随着偏度的增加和变为正数，波动率和回报之间的正相关关系变为负相关关系。对于具有正偏度的股票，较高的波动意味着较低的回报。更甚的是，拥有高正偏度和高波动率股票的投资组合获得最低的回报。

这是对最小方差的有趣扩展，与先前推测的寻求中奖投资者行为一致，细化了波动率的作用，因此更多地证实了[组合理论的死亡](https://quantivity.wordpress.com/2011/04/10/portfolio-theory-is-dead-now-what/)（同上）：

> 具有较低偏度的股票在波动性增加时获得高回报，但具有较高偏度的股票在波动性减少时获得高回报。尽管在平均-方差模型下，投资者总是更喜欢低波动而不是我们结果所暗示的高波动，但波动率的补偿反映出了一定的难题。因此，我们认为投资者之所以接受低回报和高波动，是因为他们更受高正偏度的吸引；他们是偏度爱好者或彩票投资者。

尽管这种回报-方差-偏度关系对于交易员来说是直观明显的，但这篇文章很好地将激励最小方差优化的直觉扩展到高阶矩。

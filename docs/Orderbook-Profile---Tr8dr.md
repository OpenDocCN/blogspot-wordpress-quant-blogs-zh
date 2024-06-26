<!--yml

分类：未分类

日期：2024-05-18 15:30:49

-->

# 订单簿概要 | Tr8dr

> 来源：[`tr8dr.wordpress.com/2011/01/29/orderbook-profile/#0001-01-01`](https://tr8dr.wordpress.com/2011/01/29/orderbook-profile/#0001-01-01)

2011 年 1 月 29 日 · 9:41 pm

我有一段时间没有发帖了，因为一直在忙于启动一个新的高频交易公司。我们两周前开始交易，所以将重新开始定期发帖。

在中等日频到高频空间之间有一些建模交叉，但当然这些领域都有它们自己的特点。

最高的每笔交易利润策略专注于短期跨资产关系、MR，以及长期平均预测。这些策略的持仓期为几分钟，通常在 5-20 分钟之间。话说回来，高频领域也充满了机遇。在某些情况下，交易成本后的利润可能只有几个基点，但胜率非常高。

对于一些简单的高频策略来说，解读订单簿和进出流量是关键。这里是一个订单簿概要示例，显示订单在簿中的持续时间与相对于内部价格的初始定位（就在放置之前）之间的关系。+点数位于内部价格之外，-点数优于内部（即优于最佳买入价或卖出价）。

![](https://tr8dr.wordpress.com/wp-content/uploads/2011/01/wide-profile1.png)

显然，对于这个样本，大多数订单的生存时间在从内部到内部+3 点的 15 秒至 15 分钟范围内。更有趣的是，查看这个子集中的更高频活动：

![](https://tr8dr.wordpress.com/wp-content/uploads/2011/01/short-range.png)

我们可以用这来看大多数活动发生在哪里。通过更多的分析，可以了解其他算法正在做什么以及它们在市场上的频率。看到这个随市场时间和制度的改变也是很有启示意义的。

在上面的密度图中，很容易看出在这个样本中，+5/10 个点的差价是高频算法的一个流行目标，对于订单持续时间 1 毫秒及以上。对于小于 1 毫秒的订单（基本上是紧密跟随一个取消），也有一些有趣的事情发生。然后，我们可以追踪这些订单流，针对这些目标进行查看，从而了解市场上的其他游戏。

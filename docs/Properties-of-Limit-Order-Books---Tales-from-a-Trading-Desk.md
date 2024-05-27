<!--yml

分类：未分类

日期：2024-05-18 06:36:02

-->

# 限价订单簿的性质 | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2012/08/23/properties-of-limit-order-books/#0001-01-01`](https://mdavey.wordpress.com/2012/08/23/properties-of-limit-order-books/#0001-01-01)

## 限价订单簿的性质

在阅读“限价订单簿的实证和数学性质”时，我注意到了“金融市场模型的一[族](https://www.assembla.com/spaces/MarketModel/wiki)”。尽管古老，但 FinancialMarketModel 对于任何对市场和订单簿感兴趣的人来说都是有趣的，因为该 wiki 提供了一些适当的阅读材料以及源代码。也许最有趣的是玩家功能，以及 DoubleAuctionOrderBook 提供的 basic 限价订单处理：

> [DoubleAuctionOrderBook](https://www.assembla.com/wiki/show/MarketModel/DoubleAuctionOrderBook "DoubleAuctionOrderBook") 的行为类似于典型的股票市场。一些(有耐心的)交易者放置限价订单，指定数量和价格。其他(不耐心的)交易者放置市价订单，只要存在由未决限价订单提供的充足流动性，就会立即以市场价格执行。按照挂起的限价订单数量，放置或取消限价订单需要对数时间，放置市价订单需要常数时间，清理需要线性时间。

多年来，我一直参与了许多市场项目，尽管 FinancialMarketModel 仅限于基本的限价订单，但源代码至少是公开的，玩家概念对于任何从接受测试的角度编写自己市场的人来说都是相关的。对于那些有野心的人来说，可以考虑在添加 peg 订单（或类似）方面考虑这个代码库，以开始模拟更市场的行为 - 可能考虑克隆 NYSE Euronext 的订单类型。

由 mdavey 于 2012 年 8 月 23 日发布。

发布在 [交易](https://mdavey.wordpress.com/category/trading/)

标签：[OrderBook](https://mdavey.wordpress.com/tag/orderbook/)

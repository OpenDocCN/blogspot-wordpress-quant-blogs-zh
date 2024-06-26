<!--yml

category: 未分类

date: 2024-05-18 06:44:29

-->

# 寻找低阿尔法订单：识别交易者类型第一部分|机械市场

> 来源：[`mechanicalmarkets.wordpress.com/2015/01/13/trader-type-and-order-age/#0001-01-01`](https://mechanicalmarkets.wordpress.com/2015/01/13/trader-type-and-order-age/#0001-01-01)

在交易中的一般智慧说最好的交易对象是人，而不是计算机。而且，所说的计算机是指任何机器辅助执行，不仅仅是 HFTs，还包括各种执行算法。HFTs 只有在他们认为订单会赚钱时才会（可能）进入市场，而执行算法主要用于转移大量股票，所以即使算法在其工作上不太擅长，它依然会成为一个相当具有毒性的交易对手。而人类，我期望他们对所选的价格会相当不精确（因为这不值得他们的时间），在订单和撤销的时间上更不精确（慢和不专注是作为人的一部分），并且更不太可能有计划继续朝着同样的方向交易（否则他们会找到人帮助他们得到一个良好的成交）。

因此，对于寻求长期阿尔法的计算机化交易者来说，首先要考虑的是如何最大限度地提高与人交易的机会。很可能，所有会成交的手动提交订单中，绝大多数都是市价订单——首先会成交于内部化交易商、批发商和 dark pools。然后，如果在这些市场中没有人对他们的条件感到满意，它们就会被发送到主要交易所。在那里，由于 FIFO 休息委托队列的竞争性质，要有选择性地与小额手动订单交易是极其困难的——为了挑出更高比例的有利的接收订单，交易者必须在所有试图做相同事情的机器之前先提交他们的休息委托单。鉴于市场上有如此之多又快又聪明的程序，要击败它们中的佼佼者是非常具有挑战性的。

知道有市场价的手动订单竞争非常激烈，我们现在将重点放在休息的手动订单上。为了尝试识别这些订单，我们可以考虑它们与之不同的地方，高频交易（HFTs）。HFTs 以其非常高的撤销率而闻名，这意味着它们发送到市场的绝大多数订单在执行之前都被撤销了。来自最新 ESMA 报告的下图显示了 HFTs、投资银行和其他交易者的订单寿命统计数据。请注意，在提交后 1 秒内，超过一半的 HFT 订单已被取消，但只有大约四分之一的非 HFTs 订单被取消了。这张图表来自欧洲的数据，但一般趋势应该适用于任何高频交易存在的市场。

![esma_n1_2014_c3](https://mechanicalmarkets.wordpress.com/wp-content/uploads/2015/01/esma_nov2014_c3.png)

交易类型的订单寿命分布。纵坐标是订单寿命（秒），横坐标是百分位数。[[报告链接]](//www.esma.europa.eu/content/ESMAs-Economic-Report-No-1-2014-High-frequency-trading-activity-EU-equity-markets "[报告链接]")

考虑到交易类型和订单年龄之间的相关性，让我们看看各种年龄订单执行前后市场价格的变化，从每个订单的角度来看。

![toa-orderageinet-800](https://mechanicalmarkets.wordpress.com/wp-content/uploads/2015/01/toa-orderageinet-13662.png)

顶部面板：从交易时间的角度，每股平均盈利或亏损与距离的关系，从被动交易方的角度。例如，交易后 30 秒，不到 100 毫秒的平均纳斯达克订单与最近交易的 100 股的价格相比，已经亏损了约 0.2 分（20mils）。相同测量标准下，超过 1 秒的平均纳斯达克订单已经亏损了约 0.5 分。不包括费用和折扣。数据不包括每个交易所。底部面板：纳斯达克交易股数与距离（包括受托交易）。注：每条线周围都有一个（粗略计算的）标准差宽度的阴影区域，太窄了看不见。1“mil”=每股 0.01 分。

![toa-orderagebatsz-800](https://mechanicalmarkets.wordpress.com/wp-content/uploads/2015/01/toa-orderagebatsz-13662.png)

Bats BZX 的类似图表，底部面板仍然是纳斯达克的股票交易量

当我第一次看到这种效应时，它的规模让我感到惊讶。在算法交易的宇宙中，一分钱的差异——typically HFT 利润率的数倍——是显著的。这也是一个相当明显的现象，通常当一个效率问题是如此显著时，市场会找到减少它的方法。我能想象的一个简单的应用是，许多寻求流动性的执行算法可能更倾向于与年龄更大的订单交易，潜在地为他们的客户节省一分钱。当然，这并不意味着它的效果足够大，可以构成一个盈利策略的基础，但正如我在[下一篇文章](https://mechanicalmarkets.wordpress.com/2015/01/20/identifying-trader-type-pt-2/ "Creating an HFT Strategy: Identifying Trader Type Pt. 2")中将描述的那样，就算这样，也不需要花费太多的精力就能将其实现。

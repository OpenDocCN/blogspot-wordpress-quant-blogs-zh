<!--yml

类别：未分类

日期：2024 年 5 月 12 日 19:38:55

-->

# Bloomberg 和 TradeWeb 的交易价格 | 编码市场

> 来源：[`etrading.wordpress.com/2009/09/23/bloomberg-and-tradeweb-cover-prices/#0001-01-01`](https://etrading.wordpress.com/2009/09/23/bloomberg-and-tradeweb-cover-prices/#0001-01-01)

## Bloomberg 和 TradeWeb 的交易价格

### 2009 年 9 月 23 日

在我的上一篇文章之后，我收到了有关 RFQ 的交易价格的电子邮件查询，所以我回顾了一下我在 2006 年对 RFQ 进行的一些旧分析。我的代码从 ION MarketView 的交易链中获取了与我们在 Bloomberg 和 TradeWeb 上交易的 RFQ 的交易价格。如果客户与另一家交易商交易，或者拒绝了我们的交易，我们会看到交易价格为零。这种不对称性允许交易商计算出 RFQ 胜出的过大的差额，但看不到交易离开时交易商的最佳价格有多大差距。

胜出较大的差额是胜出价格和交易价格之间的差异。如果差距太大，那么也许交易商正在遭受一种[赢家的诅咒](http://en.wikipedia.org/wiki/Winner's_curse)。显而易见的反应是降低定价的激进性。但是，RFQ 中失败的交易商看不到赢家的价格，这就阻止了这样做。在面对这种不对称性时，正确的解决方案可能是在命中率和定价激进性之间实时反馈…

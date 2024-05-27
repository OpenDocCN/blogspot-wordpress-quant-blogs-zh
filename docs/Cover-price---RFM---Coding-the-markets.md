<!--yml

category: 未分类

date: 2024-05-12 19:39:01

-->

# Cover price & RFM | Coding the markets

> 来源：[`etrading.wordpress.com/2009/09/22/cover-price-rfm/#0001-01-01`](https://etrading.wordpress.com/2009/09/22/cover-price-rfm/#0001-01-01)

## 盖板价与 RFM

### 2009 年 9 月 22 日

[这里](http://www.tradeweb.com/about/resources/brochures/institutional/credit/CDSTradingProtocolsSheetWeb.pdf)有一份精彩的文档，来自 [TradeWeb](http://www.tradeweb.com)，介绍了 CDS 执行协议。从中你可以推断出“盖板价”的定义：未成交的次佳价格。正如你可以在文档中或者在 TradeWeb 或 Bloomberg 终端中看到的那样，客户可以看到最多 5 家交易商的竞争报价。但是，在 RFQ 进行中，交易商们不能看到彼此的报价。当 RFQ 以执行结束，而不是客户拒绝时，获胜的交易商就可以看到盖板价——他们所击败的价格。但是输掉的交易商看不到获胜价格，因此存在着根本上的不对称性。

那么造成这种不对称的原因是什么呢？这是一个有趣的问题。我猜想这是由于限制交易商对彼此定价信息的了解所驱使的。交易商们对其他交易商掌握其定价信息感到非常警惕。另一个动机是保持交易商的定价敏感度。如果交易商能够看到彼此的价格，那么他们就会松懈，只提供足够赢得交易的价格。面对这两个强大的动机，我确实想知道为什么 ECN 在所有情况下都向获胜的交易商展示盖板价。

在 TradeWeb 文档中提出的 RFM 模型也很有趣。Bloomberg 和 TradeWeb 为固定收益交易运营的 RFQ 和 RFS 模型要求客户在前期声明他们是买入还是卖出。RFM 与此不同。如果将其应用于利率市场，我想知道它是否会导致更敏感的定价？

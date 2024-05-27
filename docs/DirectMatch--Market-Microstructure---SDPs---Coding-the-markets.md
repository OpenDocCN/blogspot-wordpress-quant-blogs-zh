<!--yml

category: 未分类

日期：2024 年 5 月 12 日 19:32:09

-->

# DirectMatch，市场微观结构和 SDPs | 编码市场

> 来源：[`etrading.wordpress.com/2015/01/20/directmatch-market-microstructure-sdps/#0001-01-01`](https://etrading.wordpress.com/2015/01/20/directmatch-market-microstructure-sdps/#0001-01-01)

## DirectMatch，市场微观结构和 SDPs

### 2015 年 1 月 20 日

最近我一直在忙于[SpreadServe](http://www.spreadserve.com/)，所以没有太关注我曾经[经常博客](https://etrading.wordpress.com/2007/05/24/rfs-vs-rfq/) 的[etrading](https://etrading.wordpress.com/2006/08/31/adverse-selection-and-uninformed-traders/) [话题](https://etrading.wordpress.com/2006/08/31/adverse-selection-and-uninformed-traders/)。多亏了[mdavey](https://mdavey.wordpress.com/)的一则更新，我开始赶上了[jgreco 一直发布的优秀而发人深省的内容](https://medium.com/@jgreco/internalization-and-adverse-selection-79f9fee8684d)，关于他计划建立一个[新的美国国债交易场所](http://directmatchx.com)，作为一个限价委托簿，买卖双方平等交易。我喜欢关于[内部化和逆向选择](https://medium.com/@jgreco/internalization-and-adverse-selection-79f9fee8684d)的帖子。他对[单一交易商平台](http://www.directmatchx.com/blog/single-dealer-platforms-and-adverse-selection)的观点也是有根据的，尽管我在利率交易中的经验是很难将客户流量引入 SDPs，因为它们本质上无法提供多交易商的 RFQ，这对必须出于监管原因证明最佳执行的实际资金客户至关重要。当然，如果 BrokerTec，eSpeed 和 EuroMTS 的交易商价格与主要交易所的股票价格一样公开，那么就有可能出现更多的最佳执行问题解决方案。正如 jgreco 所指出的，透明度是关键。

现在我想提出一些问题，这些问题是由 jgreco 的帖子引发的，涉及纯技术和市场微观结构...

+   [Java](http://www.directmatchx.com/careers)? 真的吗？我想知道它是否受到了[LMAX](http://www.lmax.com)的 Java 交易实现的启发，他们的自定义集合和[Disruptor](https://lmax-exchange.github.io/disruptor/)。我本来期望是 C++，但我是一个老派的 C++程序员。

+   [那真的是工作流程吗](http://www.directmatchx.com/blog/welcome-to-interest-rates-trading)？那一定是二三线银行。我所有的经验都是在一线机构，所有定价和询价处理都是自动化的。如果交易员通过语音报价，那就是银行自己定价引擎的价格。这些引擎将以 C++编写，由 Eurex 期货或 UST on the runs 驱动，并在交易员桌面上显示滚动价格。请注意，使用了混淆技术来阻止第二步：复制并粘贴报价。在花费了一大笔钱建立了利率电子交易基础设施之后，你不希望每个人都从你的彭博页面上撤出你的曲线。

+   会使用十进制定价吗，还是会延续那种过时的 1/32 的定价方式？

+   你们会如何处理结算/信用风险？每笔交易是否会产生两笔交易，与清算机构相对立？

+   你们如何转移流动性？当流动性集中在一个交易场所时，移动起来很困难。我知道的唯一案例是德国政府期货从 Liffe 转移到 Eurex。我猜美国国债流动性分散在 D2D 和 D2C 场所，所以不是集中在一个地方，这提高了 DirectMatch 捕捉部分流量的机会。

<!--yml

category: 未分类

日期：2024 年 05 月 12 日 23:30:44

-->

# 前沿三角洲：通过互动经纪 API 录音 TAQ 数据和爱立信套利研究的预告

> 来源：[`frontrunthedelta.blogspot.com/2012/01/recording-taq-data-via-interactive.html#0001-01-01`](https://frontrunthedelta.blogspot.com/2012/01/recording-taq-data-via-interactive.html#0001-01-01)

在 10 月 28 日，读者"RKB"

[询问](http://frontrunthedelta.blogspot.com/2011/09/request-arb.html#comments)

我是如何将我的数据导入 Excel 的。首先，我要向 RKB 道歉，因为我花了

*永久*

回答他的问题。

我有一个朋友开发的程序，用 Java 编写，可以记录单个和多个证券的时间和销售情况。然后，该程序将这些数据转储到一个 CSV 文件中，我用 Excel 打开。在我对价格数据进行清理和格式化后，所有的 Excel 操作都是我处理的。

我们开发的软件在左侧，有

[IB 交易工作站](http://www.interactivebrokers.com/en/p.php?f=tws&ib_entity=llc)

通过右侧的窗口显示一些通过

[IB 的 IDEAL PRO](http://www.interactivebrokers.com/en/trading/exchanges.php?exch=ibfxpro)

. 正如您所见,我对许多种货币和几个 NYMEX 天然气期货合同有数个打开的连接。

该程序记录了股票、期权、期货、期货选项、货币和组合的买卖价、买卖量、最后交易、最后量、最高、最低和收盘价。我无法强调同步组录音的重要性。使用分或甚至秒的行情报价进行套利研究的弱点是，当今高频套利交易的性质使得这些行情报价过时。您可以记录 2 秒钟的数据，其中包括 100+次的报价变化。

最后的交易从来不重要。多腿结构的最重要的方面是活跃的买价，卖价和市场深度。流动性风险已经扼杀了太多的巨人。

这是一项关于

[三角套利](http://frontrunthedelta.blogspot.com/search/label/triangular%20arbitrage)

.对于有兴趣的人，这款软件是

待售

.

应当指出，IB 并不是在今天的市场中操作的完美平台。 他们的价格更新速度为 100 毫秒，而当今很多交易发生在 10-20 毫秒的范围内。这一障碍限制了我在记录高于我能够记录的粒度的某些 HFT 策略的能力。

并为即将发布的一篇文章提供了预告

[ADR 套利](http://frontrunthedelta.blogspot.com/search/label/adr%20arbitrage)

越过爱立信的股票...

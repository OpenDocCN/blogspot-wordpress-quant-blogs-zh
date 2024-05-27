<!--yml

分类：未分类

日期：2024-05-12 23:37:40

-->

# Front-Run The Delta：使用 USD/HKD，AUD/USD 和 AUD/HKD 上的高频 TAQ 数据进行三角套利

> 来源：[`frontrunthedelta.blogspot.com/2011/06/triangular-arbitrage-using-usdhkd.html#0001-01-01`](https://frontrunthedelta.blogspot.com/2011/06/triangular-arbitrage-using-usdhkd.html#0001-01-01)

**在阅读之前请注意**

：

*这篇博文中每张图片的水印（如果你愿意这样称呼的话）都来自博客的原始 URL 和作者（一个化名）。它们并不是从其他来源转载的——它们是这篇博客和这位作者的原创作品。*

三角套利可以定义为“以第三种货币表示的第二种货币的价格，或者根据其他两种货币计算出的汇率”。例如，如果有 USD/

**HKD**

和

**AUD**

/USD 汇率。合成 AUD/HKD 交易与实时可执行的 AUD/HKD 之间具有潜在套利关系。

[Fenn，Howison，McDonald，Williams 和 Johnson（2009）](http://econpapers.repec.org/article/wsiijtafx/v_3a12_3ay_3a2009_3ai_3a08_3ap_3a1105-1123.htm)

注意：“三角套利代表了最简单的套利机会之一。然而，据我们所知，在金融文献中没有真正严格和健壮的三角套利研究。我们相信其中主要原因是缺乏具有足够高频和可执行价格的数据集。”

[异步数据](http://www.answers.com/topic/asynchronous-data)

在研究任何套利关系时都会遇到问题。无论是股票对股票，股票对期货，期货对期货，实物对现金，或者广义上说，

*任何*

套利关系。使用期末（日，分钟，秒）数据记录进行的研究存在一个问题，即一个变量可能在最后一次已知的记录间隔中具有“这个”价格，而第二个变量同样在最后一次已知的记录间隔中具有“这个”价格。问题出在两个记录的价格，虽然它们可能是最后已知的价格，但由于它们在时间段上的差异而不能可靠地使用。只有使用最精细的同步数据才能消除这个问题。

**数据。**

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi6HJ8gh-ryo1v9AKwVuezsiYVF1X-BPEYHdmSDEWltCMG6N3IE5y4lkNlJliwQ9ZwYof5tLkHaVAh7zlA_T7p_6NVXbLxK3AVIJCs42OtpwZ7Jzzj3XvEiBggoY3FzG9Dg3qHX_1YIDJE/s1600/data1.png)

以下数据集是由我的 IT 团队开发的专有程序收集的。 该软件通过直接访问 API 连接到银行间外汇市场。 在这种情况下，三种货币对的时间和成交量是同时记录和同步记录的：任何一个变量发生变化，整个数据集就被作为一个整体记录下来。 高频和同步性的记录缓解了 Fenn 等人（2009 年）在他们对 TriArb 的研究中发现的问题。

下面是合成 AUD/HKD 和实时 AUD/HKD 之间的价差。 正如您所见，套利是

[非常一致且非常坚固](http://en.wikipedia.org/wiki/Dijkstra%27s_algorithm)

“尽管一些持续时间超过 100 秒的机会似乎存在，”Fenn 等（2009）在他们的研究中写道，“对于这两组货币，95%的机会持续时间小于 5 秒，60%的机会持续时间小于 1 秒。”

（点击放大）

还有一个显著的

**流动性损失**

从上午 11:00 CST 开始，根据三种货币对的买卖价差增加，尤其是澳元/港币。 在之前所说的合成/实际套利构造中，买卖价差的增加变得明显。

买卖价差

USD/HKD：蓝

（点击放大）

**抓住机会。**

在 2011 年 1 月 24 日凌晨 1:33:55，AUD/HKD 的合成和实时关系出现了小幅中断。 平价中断是由于实时 AUD/USD 的买价从 0.98945 涨至 0.9897 引起的，增加了 0.00052。 这个买价因素导致合成 AUD/HKD 的买价调高至 7.7154，而实时 AUD/HKD 汇率则从 7.7143 上涨到了 7.7143。

**AUD/HKD 的套利差值为 0.0011**

。

（点击放大）

注意

：这个中断只持续了短短的一秒。 虽然这次机会肯定不到一秒，但我们用于收集这些数据的测试版软件并不记录毫秒级别的详细数据，这个问题已经被解决了。

这个中断的短暂持续是一个明显的入市障碍。 Fenn 等（2009）引用了 2003 年至 2005 年之间电子交易平台和交易算法的“更广泛使用”作为机会持续时间缩短的主要原因。 他们继续指出，“从 2003 年至 2005 年，日元交易的持续时间小于 1 秒的机会比例从 40%增加至 62%，瑞士法郎交易则从 41%增加至 64%，持续时间超过 5 秒的机会的比例减少了一半。”

进一步阅读

[小世界网络的集体动力学](http://www.nature.com/nature/journal/v393/n6684/abs/393440a0.html) [国际投资和贸易中的货币风险对冲](http://ideas.repec.org/p/cfi/fseres/cf090.html) [高频交易和新市场制造者](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1722924)

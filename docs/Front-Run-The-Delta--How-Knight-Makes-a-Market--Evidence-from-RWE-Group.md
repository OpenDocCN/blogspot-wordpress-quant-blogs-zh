<!--yml

类别: 未分类

日期: 2024-05-12 23:36:25

-->

# Front-Run The Delta: How Knight Makes a Market: Evidence from RWE Group

> 来源：[`frontrunthedelta.blogspot.com/2011/07/how-knight-makes-market-evidence-from.html#0001-01-01`](https://frontrunthedelta.blogspot.com/2011/07/how-knight-makes-market-evidence-from.html#0001-01-01)

热衷于在

[OTC Bulletin Board](http://www.otcbb.com/)

，还有其他知名市场，

[Knight Capital](http://www.knight.com/)

"交易或

[makes a market](http://www.knight.com/ourFirm/vsMVS.asp)

在其网站上表示拥有超过 19,000 家美国股票。 本文以及以后的帖子的目的是要审视 Knight 背后的活动的科学原理。

今天的例子是

[RWE Group](http://www.rwe.com/web/cms/en/10122/rwe/rwe-group/)

.  他们做什么以及如何做对于这个练习来说完全不重要。 今天要依靠的重要和相关数据点是价格和时间。 RWE 的价格以欧元报价，RWEOY 以美元报价，EUR/USD 同业拆借利率，和

[synchronized](http://www.highfrequencytraders.com/article/820/major-upgrade-fsmlabs-timekeeper-increases-time-precision-high-frequency-trading)

**所有三个变量的时间戳。**

**Outrights**

: 两支股票一起。

[RWE](http://www.interactivebrokers.co.uk/contract_info/v3.5/index.php?action=Details&site=IB&conid=14198&detlev=2&sess=1310425144)

(蓝色/红色)以欧元计价，02:00AM 开盘，而

[RWEOY](http://www.interactivebrokers.co.uk/contract_info/v3.5/index.php?action=Details&site=IB&conid=58593713&detlev=2&sess=1310425201)

(绿色/紫色)，以美元计价，尽管前一个小时的买卖报价相对较紧，但直到 08:30AM 才开盘。 下面的图表是 2011 年 4 月 8 日，从左到右，中部标准时间 2:00AM 到 3:00PM。

**货币**

: 通过 IB 提供的 EUR/USD 同业拆借汇率

[Idealpro](http://www.interactivebrokers.com/en/trading/exchanges.php?exch=ibfxpro&showcategories=&ib_entity=llc)

。 同一时间记录了货币和两支股票，以避免使用可能过时的报价。

EUR/USD - 8 April, 2:00AM to 3:00PM CST

**隐含价值。**

使用以欧元计价的股票价格和实时 EUR/USD 汇率，可以推导出以美元计价的股票的理论价值。

[Gagnon and Karolyi (2004)](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=577004)

提供对这种关系的详尽研究。 作者们研究的

从 1990 年到 2002 年，使用来自 39 个国家的 589 对双重上市股票的每日收盘价。虽然大多数股票对在 15 到 20 个基点（0.15%到 0.2%）的范围内波动，但作者指出，“与本地市场股票相比，跨市场股票的溢价可以高达[66%](http://quotes.nasdaq.com/asp/SummaryQuote.asp?symbol=INFY&selected=INFY)，而折扣可以高达[87%](http://www.adrbnymellon.com/files/TN7963.pdf)，但这种幅度的偏离只能持续一天。”他们推测，“价格奇偶差异、它们随时间的持久性以及超额联动与反映在国家级别和公司特定属性上的信息障碍，体现了除了套利上的制度障碍外的信息不对称以及存在[噪声交易者](http://en.wikipedia.org/wiki/Noise_trader)。”结果发现，“超额联动与全球交易在美国市场进行的比例密切相关。”[Ejara and Ghosh (2004)](http://papers.ssrn.com/sol3/papers.cfm?abstract_id=1560482)支持他们的研究并对该领域提供了重要的研究成果。

下面是以美元计价 RWE 的隐含价值结合美元计价 RWEOY 的实时报价价值。在市场做市商公司能够更容易地将一个市场的风险转移到另一个市场的重叠时段，RWEOY 市场表现最为强劲。图表右侧欧洲收盘后的 RWEOY 价差体现了这一机制。

2011 年 4 月 8 日

2011 年 7 月 15 日

寻找 RWE 的合成价值与 RWEOY 的实际价值之间的差异就是套利。在这种情况下，就像在 4 月 8 日那样

[其他](http://frontrunthedelta.blogspot.com/2011/07/etf-futures-arbitrage-fxb-and-gbp.html)

在定价参与方中，必须建立起动态库存和风险管理系统。

**重叠市场价差。**

2011 年 4 月 8 日

2011 年 7 月 15 日

进一步阅读：

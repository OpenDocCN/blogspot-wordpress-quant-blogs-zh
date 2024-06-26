<!--yml

分类：未分类

日期：2024-05-18 15:42:34

-->

# 用 Python 交易：为 TWTR 定价

> 来源：[`tradingwithpython.blogspot.com/2014/01/putting-price-tag-on-twtr.html#0001-01-01`](http://tradingwithpython.blogspot.com/2014/01/putting-price-tag-on-twtr.html#0001-01-01)

以下是我对推特估值的尝试。我想先声明：此刻我的投资组合中很大一部分是推特空头仓位，所以我的观点有些偏颇。我之所以进行自己的分析，是因为我的赌注并没有奏效，而推特在 2013 年 12 月出现了抛物线走势。所以我在这里试图回答的问题是“我应该接受损失还是坚持我的空头仓位？”。

在撰写本文时，TWTR 的交易价格约为 64 美元，市值为 347 亿美元。到目前为止，该公司还没有实现任何利润，在 2013 年亏损了 1.42 亿美元，在实现 5.34 亿美元的收入后。最后两个数字使我们每年的公司支出达到 6.76 亿美元。

### 用户价值得出的价格

推特可以与 Facebook、Google 和 LinkedIn 进行比较，以了解用户数量及其价值。下面总结了每家公司用户数量和从市值计算出的每个用户价值。（用户数量来源：维基百科，Google 的用户数量基于唯一搜索次数）

| │  │ 用户[百万] | 用户价值[$] |
| --- | --- |
| │ --- | --- | --- |
| │ FB | 1190 | 113 |
| │ TWTR | 250 | 139 |
| │ GOOG | 2000 | 187 |
| │ LNKD | 259 | 100 |

很明显，所有公司的每用户市场估值非常相似，不过我个人认为：

+   目前推特的每用户价值比 FB 或 LNKD 更高。这并不逻辑，因为竞争对手都有更有价值的个人用户数据。

+   GOOG 在从用户那里提取广告收入方面一直表现出色。为此，它有一系列高度多样化的产品，从搜索引擎到 Google+、文档和 Gmail。推特没有任何类似的产品，而其每用户价值仅比谷歌低 35%。

+   推特在扩大用户基础方面空间有限，因为它没有与 FB 或 GOOG 产品相当的产品。推特已经存在七年了，现在想要账户的大部分人都已经得到了机会。其余的人根本不在乎。

+   推特用户基础波动较大，很可能会在下一个热门事物出现时转移。

我认为在这里最好的参考是 LNKD，它在专业市场中有稳定的细分市场。按照这个指标，推特的估值**过高。**将用户价值设定为推特 100 美元，将产生一个公平的推特**46 美元的价格。**

### **未来收益得出的价格**

有足够的数据可用于未来收益的预测。我找到的最具用处的一个是

[在此](http://blogs.wsj.com/moneybeat/2013/11/06/twitter-ipo-wall-streets-revenue-forecasts/)

。

在使用这些数字的同时减去公司的支出，我假设支出保持不变，得出了这些数字：

| │  │ 银行 | 独立 |
| --- | --- |
| │ --- | --- | --- |
| │ 2013 | -51 | -43 |
| 2014 | 292 | 462 |
| 2015 | 612 | 1120 |

**净收入（百万美元）**

假设一个健康公司的最终市盈率约为 30，我们可以计算股价：

|  | 银行 | 独立机构 | 平均 |
| --- | --- | --- | --- |
| 2013 | -2.81 | -2.37 | -2.59 |
| 2014 | 16.08 | 25.45 | 20.76 |
| 2015 | 33.71 | 61.69 | 47.70 |

**基于市盈率=30 的 TWTR 价格（美元）**

再次，平均价格预估约为**46-48 美元**，这与 IPO 时的价格相当。当前的 64 美元价格**比合理价格高出约 36%**。

### **结论**

根据现有信息，对**TWTR**的乐观估值应在**46-48 美元**的范围内。没有明确的理由使其股价走高，而且有许多运营风险使其股价走低。

我的猜测是，在 IPO 过程中，足够多的专业人士已经审查了价格，将其设定在一个公平的价格水平。接下来发生的是一个没有新信息支持的非理性市场行为。只要看看在

[stocktwits](http://stocktwits.com/symbol/TWTR?q=twtr)

上的多头狂热，人们声称“这只鸟会飞到 100 美元”。纯粹的情绪化，这永远不会有好结果。

我现在唯一能做的就是言行一致，坚持我的立场。时间会证明一切。

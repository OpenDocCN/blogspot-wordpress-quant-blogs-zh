<!--yml

category: 未分类

date: 2024-05-12 20:41:35

-->

# Falkenblog: Shorting Leveraged ETF Pairs

> 来源：[`falkenblog.blogspot.com/2011/10/shorting-leveraged-etf-pairs.html#0001-01-01`](http://falkenblog.blogspot.com/2011/10/shorting-leveraged-etf-pairs.html#0001-01-01)

[ProShares](http://www.proshares.com/)

Proshares 提供了一个极其成功的一系列交易所交易基金（ETF），让人们可以轻松获得杠杆和卖空特定的股票子集。他们交易频繁，因此显然满足了消费者的偏好，但可能也迷信了投资者的更多部分。他们明确的目标是对日常基准回报相关性的追踪，使辅助考虑变得不那么重要：最大化长期回报。因此，它们在较长期内往往表现不佳，这些累积起来。我怀疑他们最终会通过如此频繁地交易来烧钱，以一种可以预见和游戏的方式。

如果 ProShares 表现不佳，这里有一个简单的套利机会。买入提供 2 倍杠杆的'Ultras'和提供相反-2 倍曝光的'UltraShorts'。同时做空这两只股票可以生成一个风险非常低的投资组合对，因为按照设计，每日一涨 1%，另一只股票几乎肯定会下跌 1%；这些头寸将互相抵消。但两者的漂移都是负的，它们在烧钱。由于 ProShares 一直忙于添加 ETF，这个模拟策略从 2008 年的 23 对开始，现在已经增加到 45 对。下面是自 2008 年以来做空 Proshares 提供的所有 Ultra 和 UltraShort 对的总回报的图表。我每周重新平衡一次。年回报率为 14%，年化标准差为 12%。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEg06P-qH9XkLwKFlAIq7lPGENKkZwPuaUFqrgxivkTVhg9xOQUwEcOvmDfn4Dr-dNPm6xYBlcwP6VFEDmQRfvo7dHRXByBA7AQpo9PxvL6NS5GqWgNuui3UuTkjEbQ9mWSB7kGskw/s1600/proshareTR.jpg)

现在，我忽略了卖空回报，对于这些可能有些是高度负面的，但总体而言，这些卖空率相当低。因为标普 500 的预期夏普比率为 0.3（超额回报 5%和标准差 15%），这是一个非常占据主导地位的策略。请注意，尽管年化波动率为 12%，但这实际上是高估了这里的风险，因为大部分波动性是“好的”：有时回报远高于平均水平。这看起来是一个相当像马多夫的策略。

另一种方法是注意到这个策略在高波动性期间和那些波动性最高的对之间效果最好。请注意，2008 年 10 月至 2009 年 3 月是这项策略的黄金时期，2011 年 8 月也是如此，那时市场动荡不安。

下面是我用的各种对的回报率，年化的。 您也可以使用这些对来自行模拟它们。我想随着时间的推移，这些 ETFs 应该会开始以低于其净资产值的折价交易，但在那之前，这是一个似乎有效的相当简单的策略。

卖空对的总回报

| pair1 | pair2 | AnnRet |
| --- | --- | --- |
| AGQ | ZSL | 31.8% |
| BIB | BIS | 3.7% |
| DDM | DXD | 9.0% |
| DIG | DUG | 18.8% |
| EET | EEV | 7.7% |
| EFO | EFU | 8.0% |
| EZJ | EWV | 6.6% |
| LTL | TLL | 16.2% |
| MVV | MZZ | 8.5% |
| QLD | QID | 10.2% |
| ROM | REW | 7.9% |
| RXL | RXD | 5.2% |
| SAA | SDD | 10.4% |
| SSO | SDS | 9.6% |
| TQQQ | SQQQ | 3.0% |
| UBR | BZQ | 1.1% |
| UBT | TBT | 4.8% |
| UCC | SCC | 7.3% |
| UCD | CMD | 6.5% |
| UCO | SCO | 5.7% |
| UDOW | SDOW | 5.3% |
| UGE | SZK | 5.6% |
| UGL | GLL | 8.1% |
| UKF | SFK | 7.6% |
| UKK | SKK | 12.8% |
| UKW | SDK | 7.9% |
| UMDD | SMDD | 5.9% |
| UMX | SMK | 5.8% |
| UPRO | SPXU | 4.5% |
| UPV | EPV | 17.0% |
| UPW | SDP | 13.8% |
| URE | SRS | 51.8% |
| URTY | SRTY | 13.9% |
| USD | SSG | 10.2% |
| UST | PST | 3.8% |
| UVG | SJF | 10.7% |
| UVT | SJH | 14.7% |
| UVU | SJL | 20.1% |
| UWC | TWQ | 2.5% |
| UWM | TWM | 12.6% |
| UXI | SIJ | 5.9% |
| UXJ | JPX | 4.7% |
| UYG | SKF | 30.8% |
| UYM | SMN | 11.0% |
| XPP | FXP | 7.1% |

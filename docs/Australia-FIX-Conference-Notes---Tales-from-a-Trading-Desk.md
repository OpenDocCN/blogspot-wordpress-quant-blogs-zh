<!--yml

类别：未分类

日期：2024 年 05 月 18 日 05:59:52

-->

# 澳大利亚 FIX 会议笔记 | 一个交易台的故事

> 来源：[`mdavey.wordpress.com/2013/10/16/australia-fix-conference-notes/#0001-01-01`](https://mdavey.wordpress.com/2013/10/16/australia-fix-conference-notes/#0001-01-01)

## 澳大利亚 FIX 会议笔记

我今天在悉尼参加澳大利亚 FIX [会议](http://www.fix-events.com/Australia/Agenda.html) 。

展区供应商应考虑用户体验在其应用程序/演示中的好处。我意识到许多供应商销售非 UI 技术，但演示确实需要一些工作，以使潜在客户能够清楚地了解数据 ROI 机会的增值。

从这些会议中提取出的几个感兴趣的内容以及通常提供的金融杂志：

+   多资产 TCA - FX 比股票更难。

+   香港的流量将大量流向澳大利亚

+   自 2013 年 3 月 31 日起，伊斯坦布尔证券交易所的股票市场交易系统，通过 FIX 接口每秒处理近 5k 个订单，且在订单流量高峰期的延迟低于 1 毫秒

+   Aquis 交易所 - 指定市场制造商在市场上持续提供双向价格，被动订单提交，任何订单或消息都不计为消息。非指定市场制造商和指定市场制造商每天可以发送多达 25k 条消息，每月费用为£2.5k。超过 25k 条消息/天，将产生每月£10k 的费用。随着流动性从£10k-20k-30k 逐步建立，最高达到每月£50k

+   打击瓶颈：对新的 Eurex [平台](http://www.automatedtrader.net/articles/analysis/144302/battling-the-bottleneck-an-analysis-of-the-new-eurex-platform) 的分析

+   生活在[缓慢](http://www.automatedtrader.net/articles/exchange-views/144193/life-in-the-slow-lane)的车道上 - 减速带来平等的延迟游戏。EBS 实时市场数据的成本约为每月$50k，每 100 毫秒发送一次关于进货单和价格的更新。从伦敦到纽约的数据传输需要 33 毫秒，因此超过 30 毫秒的减速带从地理位置的角度打开套利机会。

+   市场数据的组播传递。

+   放弃 HSRP（热备份路由器协议），损失 1.5 毫秒。放弃 NAT（网络地址转换）并获得另外 500 微秒。

+   智能订单路由场所访问顺序很重要

+   哪些信息对赋予买方交易员权力至关重要 - Thomas S. Kingsley，亚太执行咨询和交易主管，彭博交易所

+   算法策略 - IS，VWAP，TWAP，目标收盘价，参与/伴随成交量，黑暗汇总/互动/流动性驱动/信号驱动，自定义

+   一些经纪人提供查看算法的能力，并实时或事后查看其操作情况 - Jason Lapping，亚太交易主管，Dimensional（澳大利亚）

+   -  未来：自适应算法，利用统计分析提前查看策略 – 托马斯·S·金斯利，Bloomberg Tradebook 亚太区执行咨询与交易负责人

-  主题演讲：市场发生了地震性变化？你准备好了吗？ – 赛斯·梅林，Liquidnet CEO 和创始人：

+   -  幻灯片演示很不错 – 除了一些图表图像

+   -  随着利率上涨而产生的大规模资产配置转变

+   -  资产配置“你可以投资于股票，可能会亏钱，或者投资于固定收益产品，肯定会亏钱”

+   -  监管可能是一种限制也可能是一种促进

+   -  设计或默认的市场结构 – 美国是默认的。澳大利亚以身作则 – 市场结构，为未来投资。

+   -  为批发市场创建的匿名性、规模和价格改善的暗池

+   -  更有效的市场 = 价格发现 + 规模发现

-  外汇交易成本分析（TCA）：

+   -  用于外汇的哪种基准？当天的最高/最低价？随时间的最高/最低价？

+   -  VWAP/TWAP 也可能是[TCA](http://www.fxweek.com/fx-week/feature/2183429/standards-multiply-tca-takes-hold) 的适当基准

+   -  与股票不同，外汇因托管人（执行性能）而变得复杂。此外，在外汇领域，什么是交易日的定义？不同地区的托管人是否有不同的交易日？

+   -  FX TCA 现货的可能解决方案 – [桶](http://www.e-forex.net/articles/free/Special+Report/1852/Introducing+benchmarks+into+the+FX+trade+execution+process) 交易：无限制货币，通过托管人限制货币，通过托管人进行外汇交易

+   -  性能分析 – 帮助为外汇定价过程带来[透明度](http://www.financial-journalist.co.uk/financial_journalist/finance/performance-analytics-helping-to-bring-transparency-to-the-fx-pricing-process/)

-  由 mdavey 于 2013 年 10 月 16 日撰写。

-  发布在[交易](https://mdavey.wordpress.com/category/trading/)类别中

-  标签：[TCA](https://mdavey.wordpress.com/tag/tca/)

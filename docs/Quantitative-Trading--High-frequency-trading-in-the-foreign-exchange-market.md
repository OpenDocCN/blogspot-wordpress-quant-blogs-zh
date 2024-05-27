<!--yml

分类：未分类

日期：2024-05-12 19:01:55

-->

# 量化交易：外汇市场的高频交易

> 来源：[`epchan.blogspot.com/2012/03/high-frequency-trading-in-foreign.html#0001-01-01`](http://epchan.blogspot.com/2012/03/high-frequency-trading-in-foreign.html#0001-01-01)

这是标题的一个

[报告](http://www.bis.org/publ/mktc05.pdf)

由国际清算银行（为世界各地的中央银行服务）于 2011 年 9 月发布的。作为一个外汇交易员，我当然非常关注它，希望能瞥见 whatever 是最新技术。以下是一些有趣的小片段，以及我的评论：

1) 外汇高频交易（FX HFT）的延迟时间小于 1 毫秒，而我们这些普通算法交易员通常至少要承受 10 毫秒的延迟。例如，Interactive Brokers 尚未为其客户提供托管设施，因此我们最好的做法是将交易服务器放在互联网骨干上，靠近其在康涅狄格州斯坦福的位置。最佳往返 ping 时间是 10 毫秒。那些与 FXCM 交易的人可能有更低延迟的机会，因为他们提供

免费

向客户提供托管服务。那些在 ECN FXall 上交易的客户

[在他们 Equinix 数据中心托管](http://www.equinix.com/company/news-and-events/press-releases/americas/2009/fxall_offers_foreign_exchange_platform_en/)

，而

[FCM360](http://www.fcm360.com/financial-industry-solutions/foreign-exchange-hosting-colocation-connectivity/icap-ebs-servers/)

为 EBS 交易者提供托管服务。我找不到任何为 Hotspot FX 或 Currenex 提供托管服务的内容。如果你知道这样的服务，或者外汇经纪商提供托管服务，请留下评论！

2) 高频交易通常在流动性高、波动性低的市场中操作。前者并不令人惊讶，因为波动性低的市场成交对手较少。后者需要一些细微的差别。我认为大多数高频交易在平均回归市场中从高波动性中受益，但不幸的是，高波动性通常与市场自由落体相关。所以如果你发现市场压力下高频交易提供的流动性突然消失，不要感到惊讶，尽管 BIS 报告指出，他们在市场动荡结束后很快就会重新进入市场。

3) 作为 2)的推论，高频交易（HFT）主要交易于主要货币对。但越来越多地，NZD 和 MXN 吸引了众多自动化和高频交易者。

4) 几乎可以定义，高频交易放置的买入/卖出报价在簿上保留的时间非常短，以毫秒计，除非交易所强制其保留更长时间。EBS 和路透社都有最小报价生命或最小填充率。一个交易所确实

不是

有这样的最小值，那就是 Currenex，因此对高频交易特别有吸引力。因此，如果你不是高频玩家，并且不希望被高频玩家利用，要小心 Currenex！

5) 高速交易策略（HFT）最喜欢的两个类别：三角套利和流动性再分配（利用不同交易平台之间的定价差异）。尽管在过去几年中，HFT 从业者获得了不佳的声誉，但我认为他们通过这两个策略为像我这样的其他算法交易者提供了有用的服务。不断寻找更适合自己策略的经纪商/价格是一件麻烦事！

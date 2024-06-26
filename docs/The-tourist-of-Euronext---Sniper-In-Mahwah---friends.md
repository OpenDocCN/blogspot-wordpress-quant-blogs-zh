<!--yml

分类：未分类

date: 2024-05-18 14:13:08

-->

# 欧罗纳斯特游客——萨米普尔·在马瓦赫与朋友们

> 来源：[`sniperinmahwah.wordpress.com/2015/12/10/the-tourist-of-euronext/#0001-01-01`](https://sniperinmahwah.wordpress.com/2015/12/10/the-tourist-of-euronext/#0001-01-01)

终于，有关高频交易（HFT）在法国有所行动。法国金融市场管理局（AMF）最近对一家交易公司维图（Virtu）和一家交易所欧罗纳斯特（Euronext）进行了罚款。AMF 发布的关于此案件的全报告/处罚，用法语，请[点击这里](http://www.amf-france.org/Sanctions-et-transactions/Decisions-de-la-commission/Chronologique/Liste-Chronologique/Sanction.html?year=2015&docId=workspace%3A%2F%2FSpacesStore%2F079a99f9-ae7d-4786-ad5a-ef55ad788145)。以下是这个案件的非常简短的总结，有一些数字。

###### -   **CONTEXT**

麦迪逊泰勒欧洲（MTE）于 2008 年 4 月作为纽约 based 麦迪逊泰勒控股公司（Madison Tyler Holdings LLC）的子公司成立，2011 年与维图金融公司（Virtu Financial）合并。2009 年，麦迪逊泰勒欧洲在伦敦设有办事处，一打员工为该公司的自营交易部门工作。追溯到 2008 年 6 月，MTE 成为欧罗纳斯特的会员，2009 年 1 月 MTE 开始在巴黎郊区的奥贝维利埃将他们的服务器与欧罗纳斯特匹配引擎近距离部署（后来，在 2010 年，欧罗纳斯特搬到了英格兰巴 ildon，那里交易所建立了一个新的数据中心）。

根据 AMF 的说法，欧罗纳斯特最初没有对向交易所发送订单的公司收费，但由于新的电子（HFT）生态系统，欧罗纳斯特平台无法管理订单流量，决定为每个成员设定每日订单与交易比率（OTR）（并对每个新订单征收罚款）。AMF 表示，2008 年 1 月欧罗纳斯特的 OTR 为 10（订单）/1（交易），2009 年 3 月改为 100/1（此后比率保持不变）。欧罗纳斯特对在流动性较弱的股票中“提供流动性”的公司有一个特殊计划（作为回报，市场制造商收到了费用折扣）但在 2009 年没有向交易前 100 只非常流动的股票（“欧罗纳斯特 100”）的公司提供此类计划。

###### -   **INVESTIGATION**

2010 年，法国金融市场管理局（AMF）开始对 MTE 的所谓“分层”活动进行调查（分层被认为是当一家公司向交易所发送订单，但取消这些订单，仿佛它们从未打算被执行时的一种操纵性计划）。鉴于涉及的数据量巨大，AMF 只对 27 种不同且流动性强的股票（主要是法国公司，如法国电信、标致、法国电力公司，甚至还有一家银行，法国农业信贷银行）进行了调查；鉴于 MTE 在这些股票上与其他交易所（BATS、Chi-X、纳斯达克欧洲和土库曼斯坦）的数据无法同步，调查集中在 2009 年 7 月 21 日至 9 月 2 日的 32 个交易日内（特别关注的一天是 8 月 28 日，关注的是一只股票，法国电力公司）。

###### FINDINGS

首先，报告中提到 MTE 收到消息确认（交易/取消确认等）在大约 5 毫秒后这些消息被发送到 Euronext 的其他成员，这种政策，允许一家公司“看到市场”在其他参与者之前，已经引起了市场微观结构专家的广泛讨论，一些交易所没有同样的政策——据我所知，在 Eurex 上，消息是同时发送给所有参与者的。这一点很重要，因为根据 AMF 的说法，2009 年 7 月至 9 月，MTE 在 Euronext 上发出的 500 万个订单在 2 毫秒内被取消/修改，这意味着当其他成员收到这些消息时，这些订单已经消失了。

AMF 主要关注一个名为“Soap”的 MTE 算法（另外两个类似的算法“Tourist”和“Schwamm”（德语中的“Sponge”），也涉及其中）。简而言之，Soap 1) 在五个交易所中的*一个*上检测股票的最佳价格（Euronext、BATS、Chi-X、Turquoise 或 Nasdaq Europe）；2) 将被动订单发送到*四个*其他平台；3) 检查这些四个订单中是否有一个被执行；4) 如果是这样，那么 Soap 在其他平台上下单；5) 回到 1)。平均订单量为±100-400 股；80%的交易在不到 1 秒内执行（66%在 10 毫秒内）；MTE 在 90%的交易中获利。

此外，2009 年 8 月 28 日对 EDF 股票的特殊调查显示

– MTE 向五个交易所发送了 576237 条消息（其中 206133 条发送给了 Euronext）

– 成交了 1506 笔订单（其中 605 笔在 Euronext 上）

– 订单成交比率为 Euronext 上的 341/1，BATS 上的 2358/1，Chi-X 上的 120/1，Turquoise 上的 495/1，Nasdaq Europe 上的 1249/1

– 在 Euronext 上，MTE 占消息量的 81%，但成交量为 2.8%；在 BATS 上，MTE 占消息量的 93.6%（成交量为 17.6%）；在 Turquoise 上，MTE 占消息量的 58%（成交量为 11.2%）

###### **罚款**

简而言之，Euronext 被罚款是因为该交易所允许 MTE 的订单成交比率超过 100/1，并未以*清晰明了的方式*告知其他参与者（尽管 AMF 承认，还有三家其他 Euronext 成员，未公开名称，也拥有超过 100/1 的 OTR）。在 AMF 分析的 32 天里，MTE 的订单成交比率为 253/1（MTE 对这一比率提出异议，称 OTR 为 146/1），而其他成员的平均成交比率为 11.7/1。AMF 估计 Euronext 给予 MTE 的非公开豁免导致了交易所 1.9 亿欧元的损失（MTE 应支付的罚款金额）。AMF 因此对 Euronext 罚款 5000 万欧元，因为该交易所没有尊重“*其中立和公正的职责*”。

MTE（现更名为 Virtu）还因“*市场操纵*”被罚款 500 万欧元——法国金融市场管理局（AMF）估算，在 32 天里，得益于 Soap、Tourist 和 Schwamm，MTE 的利润达到了 78.2 万欧元。Virtu 回应称算法在不同交易所之间进行了“*套利*”（“*套利者在一个平台上购买低估的股票，然后在股票被高估的地方出售它们*”）,并辩称这种“*流动性转移*”允许其他参与者节省 250 万欧元。但 AMF 并不认同。考虑到很多交易公司（无论是否为做市商）都在使用同类型的算法，我在想 AMF 将如何处理所谓的“分层”操纵。Virtu 和 Euronext 都在上诉 AMF 的决定。这个案件还将持续数年。希望它能帮助人们更好地理解做市商是如何运作的。

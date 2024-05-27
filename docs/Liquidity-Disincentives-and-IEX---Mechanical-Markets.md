<!--yml

分类：未分类

日期：2024-05-18 06:38:14

-->

# 流动性抑制措施与 IEX | 机械市场

> 来源：[`mechanicalmarkets.wordpress.com/2017/08/14/liquidity-disincentives-iex/#0001-01-01`](https://mechanicalmarkets.wordpress.com/2017/08/14/liquidity-disincentives-iex/#0001-01-01)

交易所费用计划可能是市场结构中最无聊的话题。但是，偶尔会有几乎有趣的异常情况，比如 IEX 的新[费用](https://www.iextrading.com/docs/rule-filings/SR-IEX-2017-27.pdf)。本质上，新费用将对流动性接受者在 IEX 完成执行时“崩溃报价指示器”处于开启状态时收取额外的 30 毫秒。 [1][2] 大多数交易所通过激励措施分段订单流量；IEX 试图通过使用抑制措施来开辟一个利基市场。

有了这项费用，IEX 似乎故意针对那些他们认为正在损害其市场的交易者。John McCrank[转达](https://www.reuters.com/article/us-usa-trading-iex-group-idUSKBN1AR2CH)了 IEX 的 Eric Stockland 以下的话：

> 如果我们能阻止高频交易市场制造商被掠食者策略捕食，那么副产品应该是更多的流动性和更好的交互体验

IEX 的[文件](https://www.iextrading.com/docs/rule-filings/SR-IEX-2017-27.pdf)明确指出，费用目标是“仅 13 名成员...可能会从事针对即将过时的价格的休息订单的故意策略。”

我们[讨论](https://mechanicalmarkets.wordpress.com/2015/08/11/iex-ideology-and-the-role-of-an-exchange/)过交易所对“即将过时”的价格进行处罚的独特性，这个词语几乎是一个矛盾修辞。在一个健康的市场中，成交量和价格变化是不可分割的：当交易者认为价格即将上涨时买入，而价格上涨通常是在买方启动交易后。这些过程是市场的自然特征，通常只能通过交易阻止价格控制来防止。因此，我发现 IEX 的[目标](https://www.iextrading.com/docs/The%20Evolution%20of%20the%20Crumbling%20Quote%20Signal.pdf)“防止某人*预期* NBBO 的变化”非常奇怪。

我内心的一部分怀疑 IEX 真正希望做的是将最后查看[功能](https://mechanicalmarkets.wordpress.com/2015/10/05/iex-peg-orders-last-look-for-equity-markets/)将其 peg 订单的流动性展示出来，但这样做可能对他们来说过于[有问题](https://mechanicalmarkets.wordpress.com/2016/10/24/chx-and-four-types-of-speed-bump/)。Brad Katsuyama[告诉](https://www.bloomberg.com/news/articles/2016-10-12/beyond-flash-boys-matt-levine-interviews-iex-s-brad-katsuyama)Matt Levine：

> “人们问我们为什么不让 D-peg 成为一个显示订单。这变得非常具有挑战性……在显示流动性的背景下——看到某样东西然后它对你消失——我们一直非常意识到这就是我们整个旅程的开始。我们不想对此做出贡献。”

因此，IEX 选择对接受方收取[法定最高](https://www.law.cornell.edu/cfr/text/17/242.610)的费用，而不是允许显示订单在“报价不稳定期间”消失。

现在，IEX 当然知道会支付这笔费用的 13 个会员的身份。Stockland 表示，这笔费用针对的是“掠夺性”的高频交易策略 [3]，并旨在帮助其他高频交易策略。交易所可以自由地对其想要鼓励或抑制的高频交易类型做出善意判断，但 IEX 继续使用富有情感色彩的语言。我希望他们的感情在决定中没有起到作用。

在任何情况下，如果费用成功并且市场制造商在 IEX 上报价更多的显示流动性，那么支付费用的交易者组成很可能会发生变化。我坚信，如《[闪购男孩](https://www.nytimes.com/2014/04/06/magazine/flash-boys-michael-lewis.html)》一书中描述的 Thor 路由器，会为其大多数符合条件的订单支付这笔费用。如果 Thor 清扫了纳斯达克的簿记，IEX 很可能会认为报价“正在崩溃”，因为 Thor 的订单离开了 IEX 的速度障碍。Thor 似乎是为点击交易者设计的，因此它可以额外延迟 350 微秒发送其订单到纳斯达克和 Bats，这样 IEX 就无法在执行后意识到报价即将“崩溃”。但是许多智能订单路由器和执行算法在市场活跃期间交易，而且不能不经历滑点就延迟它们的订单。 [4]

# 显示流动性和上市情况

IEX 迫切需要增加他们市场上的显示流动性。原则上他们可能不[介意](https://medium.com/boxes-and-lines/focusing-on-price-discovery-d99951ec4df4)成为一个[主要](https://twitter.com/sumohurd/status/892348644271075329)的暗池，但如果他们想要吸引[上市](https://www.ft.com/content/f9a7b332-7bbe-11e7-9108-edda0bcbc928)的话，他们需要让发行者相信他们能够实际地促进价格发现。坦白说，IEX 当前的预交易透明度水平令人尴尬，任何选择在那里上市的发行动作都存在严重风险。我怀疑 IEX 知道这一点，新的费用安排是对显示报价的真正激励。

这并不意味着它会起作用。IEX [认为](https://medium.com/boxes-and-lines/focusing-on-price-discovery-d99951ec4df4)他们[拒绝](https://www.ft.com/content/4c805dd6-449f-11e7-8519-9f94ee97d996)支付回扣是他们的交易所大部分时间处于黑暗状态的原因。 [5] 新的费用可能的另一个目的是增加对降低访问费用上限的支持。费用及其任何模仿者可能会让目前对访问费用上限漠不关心的市场参与者感到不满。将[当前上限](https://www.law.cornell.edu/cfr/text/17/242.610)从 30 毫秒降低将减少交易所能够支付的回扣。如果 IEX 的说法是真的，结果将提高他们展示的市场份额。我有点怀疑：我怀疑 IEX 在展示流动性方面遇到困难，因为他们的最后查看功能允许暗订单优先与低α攻击者交易，将异常高的α流量留给他们的公开报价。

# 为事后市场变动向交易员收费

新的费用取决于订单发送后的市场状态。如果访问费用上限更高，这将使定价经济上等同于最后查看。但即使当前上限如此，也存在一些奇怪的可能性。如果允许这种费用，有什么能阻止交易所征收一个未来一毫秒内市场变化的费用呢？或者第二？或者一天？例如，交易所可能会对跟随看涨价格变动超过 0.1%的交易收取额外的 30 毫秒。利用产生的收入，它可以在波动时刻向被穿透（例如，1%）的挂单支付巨额回扣，补偿市场制造商的损失。这可能会在交易量大的时期使交易所的订单簿更厚，从而获得市场份额。很容易看出这种定价方式如何反噬，如果尾部事件在加厚的订单簿上发生，交易所可能需要支付比预期更大的费用。而支付给交易员的钱因为他们错了而感到不舒服。但发行人可能喜欢这种诱人的可能性。

交易所也可以尝试相反的做法，即为正确的预测支付高α交易员的费用，并对噪音交易者进行惩罚。很可能会有一些噪音交易者转移到其他场所，只留下由自信的参与者发送的订单。这将为场地的分割光谱增加另一个层次。在当前体制下，低α流量不成比例地被引导到内部化和批发商，迫使高α交易员在公开交易所相互交流，公开交易所是价格发现的中心。或许会有少数超高级α交易员被这种新的场地的最后手段所吸引，特别是在价格处于过渡期时。我不认为大型交易所引入这种类型的伪[罪恶税](https://en.wikipedia.org/wiki/Sin_tax)是明智的，但或许像 PSX 或 EdgeA 这样的小型场所会尝试一下。

我通常对复杂的交易所逻辑持怀疑态度，但要看这种定价方式的后果还需要时间。IEX 的提议表明，他们开始像他们的竞争对手那样思考，并且以其他交易所无法做到的方式将其扭曲。这可能不符合长期交易者的口味，但毫无疑问，IEX 正在逐渐变得更加复杂。 [6]

[1] 文件称，当“在报价不稳定期间吸收流动性，如 IEX 规则 11.190(g)所定义”时，如果这类执行的成交量超过会员在 IEX 的总月执行量“5% [和] 至少 100 万股，按 MPID 基础计算。”

[2] Matt Hurd [不喜欢](https://meanderful.blogspot.com.au/2017/08/iex-fee-regression.html)新的定价。有关“崩溃报价指标”的更多详细信息，请参见他的[分析](https://meanderful.blogspot.com.au/2016/07/iex-discretionary-peg-dpeg-calculation.html)和[更新](https://meanderful.blogspot.com.au/2016/12/iex-innovation-killing-innovation.html)关于 IEX 用来判断报价是否“崩溃”的对数回归。回归使用非延迟市场数据，这些数据比交易者的订单晚 350 微秒到达 IEX。

[3] IEX 透露，最大的交易者在新费用计划下，整个 6 月将支付约 12 万美元（[脚注 17](https://www.iextrading.com/docs/rule-filings/SR-IEX-2017-27.pdf)），假设这些受到指责的交易完成了 3000 万股，那么他们的利润将约为每月 12 万美元。

[4] IEX 似乎认为任何受到费用影响的交易者，包括这些 SORs，“降低了市场的质量。”并且“理想情况下，这项费用将不会应用于任何人，因为参与者将调整其交易活动以适应定价变化。”我可能错了，但我怀疑许多经纪人不同意。

[5] IEX 的高管们反复将返利称为“回扣”。Matt Hurd [认为](https://meanderful.blogspot.com.au/2017/06/rebate-trafficking.html)，如果一个支付是回扣，那么提供免费服务也是：

> IEX 未能认识到，对于 lit 在 IEX 的零定价符合他们自己对于回扣的描述，因为回扣是一种报酬性的，而非货币性的交换。免费提供的东西，比如订单执行，也可能被视为回扣；同样，打折商品也可能算作回扣。所以如果返利是回扣，那么 IEX 也在提供回扣。这变成了一个程度问题。

[6] 值得反思的是“闪购男孩”，它[评论](https://books.google.com/books?redir_esc=y&id=UcIkAwAAQBAJ&dq=editions%3A36ZaAiOcQqEC&q=%22just+three+order+types%22)：

> 创造公平是相当简单的……他们不会向发送订单的经纪人或银行支付回扣；相反，他们会向交易的双方收取相同的手续费：每股百分之一九十毫（简称 9“毫”）。他们只允许三种订单类型：市价订单、限价订单和中间点挂单。

IEX 自那时以来已经取得了长足的进步。

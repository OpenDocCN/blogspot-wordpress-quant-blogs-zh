<!--yml

category: 未分类

date: 2024-05-18 06:39:38

-->

# CHX 和四种速度障碍 | 机械市场

> 来源：[`mechanicalmarkets.wordpress.com/2016/10/24/chx-and-four-types-of-speed-bump/#0001-01-01`](https://mechanicalmarkets.wordpress.com/2016/10/24/chx-and-four-types-of-speed-bump/#0001-01-01)

速度障碍是市场结构中的最新潮流，正在蔓延。芝加哥证券交易所（CHX）最近在美国股票市场提出了一种新型速度障碍，称为“[流动性接入延迟](http://www.chx.com/chxltad/)”（LTAD）。[1] SEC 是否批准 LTAD 的决定可能对市场结构产生重大影响，可能比 IEX 的决定更大。

要理解批准 LTAD 的后果，我认为考虑四种类型的不对称访问延迟是有帮助的：[2][3]

1.  交易所对正在访问待处理流动性的订单应用延迟。挂单本身可以在没有延迟的情况下修改或取消。这就是 LTAD。

1.  与#1 相同，只是非显示的挂单避免了延迟。

1.  延迟适用于发送到交易所的所有客户消息，包括取消和可交易订单。但是交易所运行算法订单类型，这些类型的订单会调整其属性而无需延迟。特别是，显示订单可以与未延迟的价格数据保持连接，而其潜在交易对手则受到延迟的影响。

1.  与#3 相同，只是非显示算法订单类型避免了延迟。这就是 IEX 的速度障碍。[4]

下表显示了速度障碍组合，按照哪些类型的挂单具有类似于[最终检查](https://mechanicalmarkets.wordpress.com/2015/10/05/iex-peg-orders-last-look-for-equity-markets/)的功能进行划分：

| **最终检查** | 可适用于显示报价 | 只能适用于非显示报价 |
| --- | --- | --- |
| 由挂单发送方自行决定 | #1（LTAD） | #2 |
| 由交易所算法自行决定 | #3 | #4（IEX） |

在我看来，所有四种类型都对市场最终用户造成更多伤害而不是好处（在 Reg NMS 的背景下）——每一种方式都允许挂单流动以某种方式减少。但许多最终用户持不同意见，并要求 SEC 批准#4。因此，既然速度障碍存在，非显示的挂单可能会跳过它们，那么其他三种不对称延迟中应该允许哪一种呢？

一种观点是，交易所有责任尽可能保护其固定订单。将这一原则与新的“最低限度”[解释](https://www.sec.gov/news/pressrelease/2016-123.html)相结合，可能意味着应该允许类型#3 和#4 的速度障碍。Healthy Markets 持这种观点。[5] 我认为让交易所算法具有不提供给交易者的时间优势是一个坏主意。交易所既没有激励也没有专业知识来优化其定价算法。[6] 交易所的传统角色是为买家和卖家提供一个交易场所，让他们以自己选择的价格交易。交易所主要为方便起见提供算法订单类型（如固定），我不认为应该有任何幻想认为这些订单类型与精明经纪人和交易者使用的技术一样好。为交易所算法提供时间优势意味着它们将击败交易者，在定价准确性、压力下的稳定性和多样性方面交易者是优秀的。交易者及其算法确实会犯错误，但很难相信交易所算法的单一文化会做得更好。补贴劣质的商业方法会降低行业的生产力，给予交易所算法结构性优势也不例外。

在我看来，如果允许#4，那么应该允许#2。而且，如果允许#3，那么应该允许#1。由于#4 已经获得批准，唯一需要考虑的是是否应该允许延迟对访问**显示的**报价的影响具有不对称性。[评论](https://www.sec.gov/comments/sr-chx-2016-16/chx201616.shtml)大多数情况下都很好地解释了为什么不对称性对于显示市场结构是有问题的。[7] 简而言之，如果显示订单被额外给予时间来决定是否成交交易，那么大量的报价将实际上无法访问，即使锁定、交叉或通过这些报价进行交易是被禁止的。[8] 即使在没有这些规定的市场，比如外汇市场，最后一次询问也会引起[困难](https://www.ft.com/content/875640f0-a325-11e5-bc70-7ff6d4fd203a)。[9] 将最后一次询问与订单保护结合起来的后果是不可预测的，但它们似乎不太可能对长期交易者产生好处。

因此，如果我们不希望 Reg NMS 订单保护适用于具有最后一次询问资格的报价，只有选项#2 和#4 应该被允许。然而，存在一种权衡。只给予隐藏订单时间优势将会激励黑暗交易。我怀疑主要交易所会变得像[IEX 一样黑暗](http://meanderful.blogspot.com/2016/10/iex-dark-and-expensive.html)，但股票市场可能会变得不那么透明。

IEX 的批准已经激发了复杂性的显著增加。 CHX 可能不是最重要的交易所，但与 IEX 一样，它所设立的任何先例都适用于其他交易所。[10] 将速度减缓不对称性限制在隐藏订单中存在缺点，但这可能是 Reg NMS 保持蹒跚前行的唯一方式。

[1] 从技术上讲，这并不是真正的新事物。 LTAD 类似于纳斯达克的 PSX 提出的一个[提案](https://www.sec.gov/rules/sro/phlx/2012/34-67680.pdf)，该提案被 SEC 拒绝了。

[2] 为了突出基本要素，我忽略了一些细节。

[3] 当然还有其他类型的速度减缓。例如，一个交易所可以延迟交易员取消挂单，但允许市场订单不受延迟地执行。这种延迟可以用来解决关于“[流动性褪色](https://epta.fia.org/articles/liquidity-and-quote-fading)”的投诉，并且在某些方面类似于纳斯达克的试行性“[Extended Life Order](http://business.nasdaq.com/marketinsite/2016/Enhancing-Long-Term-Liquidity-Nasdaq-Introduces-the-Extended-Life-Order.html)”和 EBS 的“[Minimum Quote Life](http://www.ebs.com/~/media/Files/I/Icap-Ebs/rulebooks/201603-05-EBS%20Dealing%20Rules%20EBS%20Market%20Appendix%20291015.pdf)”。

市场数据的延迟是完全不同类别的路障。在美国股票市场中，这些被禁止（我认为），要求[报价](https://www.law.cornell.edu/cfr/text/17/242.604)和[交易](http://www.finra.org/industry/trade-reporting-faq#102)必须立即发布到 SIP。尽管这种要求可能不适用于“最低限度”延迟？

[4] 算法订单类型也可以利用它们未延迟的数据源与不能取消的挂单进行激进交易。 IEX 的 DPEG 通过其“book recheck”[机制](https://mechanicalmarkets.wordpress.com/2015/08/11/iex-ideology-and-the-role-of-an-exchange/#3iex2)实现了这一点。

[5] 从他们的评论[信函](https://www.sec.gov/comments/sr-chx-2016-16/chx201616-8.pdf)中：

> 时间延迟不应影响交易所代表所有参与者定价订单的能力（即固定定价）。

Dave Lauer 在 Twitter 上[澄清](https://twitter.com/DLauer/status/788021717922906112)，这一原则也适用于显示的固定定价订单。

[6] CHX 对 LTAD 的辩解引发了一个有用的思维实验。CHX[认为](http://www.chx.com/_posts/rule-filings/ProposedFilings/CHX-2016-16.pdf)其 ETF 报价是“延迟套利”的受害者，而 LTAD 将防止这种情况发生。如果 SEC 拒绝 LTAD，CHX 可能会提出另一种类型的速度限制，即 CHX 通过将 ETF 中显示的订单（例如 SPY、QQQ 等）与未延迟的 CME 市场数据进行匹配来管理。CHX 是否会像专业交易员一样理解这些 ETF 与期货市场之间的关系呢？而这些 ETF 只是简单的案例 — 想象一下交易所可能会想出怎样的匹配措施，以防止在原油价格或 CVX 走势变动时市场做市商在 XOM 上遭到“撬掉”。“我相信交易所可以想出市做商会觉得很有用的匹配算法，但这真的是我们希望交易所[做的事情](https://mechanicalmarkets.wordpress.com/2015/08/11/iex-ideology-and-the-role-of-an-exchange/)吗？

[7] 谈论 LTAD 是不完整的，如果没有提及 CHX 的[市场数据分享方案](http://www.chx.com/chxshare/)。不过，这篇文章并不打算进行完整的讨论。许多的[评论信](https://www.sec.gov/comments/sr-chx-2016-16/chx201616.shtml)（以及 Matt Hurd 的充满趣味的[摘要](http://meanderful.blogspot.com/2016/10/chx-price-taking-access-delay-ltad.html)）都涉及了这个问题。

我发现有趣的是，Virtu 在 LTAD 被宣布时就[公开支持](http://www.bloomberg.com/news/articles/2016-08-30/chicago-stock-exchange-targets-latency-arbitrage-with-speed-bump)它，这可能是在他们有时间审阅文件之前。LTAD 是在 Virtu 的要求下提出的吗？Virtu 在 CHX 的盈利是否依赖于市场数据的分享？

[8] 前提是不使用 ISOs。如果足够多的显示订单被允许最后一次观望，那么市场将充斥着无法接触的行情。只有具备合法基础设施以提交 ISOs 的交易员才能在股票市场中来回。

[9] 这种看法并非一致。一些长期交易者欣赏最后一次观望，比如挪威的 SWF，[NBIM](https://www.nbim.no/en/transparency/asset-manager-p[...]erspective/2015/the-role-of-last-look-in-foreign-exchange-markets/)。

[10] 詹姆斯·安杰尔的[信件](https://www.sec.gov/comments/sr-chx-2016-16/chx201616-11.pdf)认为，CHX 应该像 IEX 一样得到宽容。我不是律师，而且我认为 LTAD 可能会伤害长期交易者，但他的一些论点是有说服力的。

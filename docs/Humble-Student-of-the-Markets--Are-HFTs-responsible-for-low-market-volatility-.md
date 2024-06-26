<!--yml

分类：未分类

日期：2024-05-18 03:19:27

-->

# 市场谦卑的学生：HFT 是否导致了市场波动性降低？

> 来源：[`humblestudentofthemarkets.blogspot.com/2015/06/are-hfts-responsible-for-low-market.html#0001-01-01`](https://humblestudentofthemarkets.blogspot.com/2015/06/are-hfts-responsible-for-low-market.html#0001-01-01)

我收到了许多关于上篇关于股票波动性下降的文章的深思熟虑的回复（见

[量化交易员会再次引爆市场吗？](http://humblestudentofthemarkets.blogspot.com/2015/06/will-quants-blow-up-markets-again.html)

). 在评论中被多次提及的一个主题是将 HFT 算法视为低波动性制度可能的原因。

表面上看，HFT 的解释是有道理的。在“正常”市场期间，HFT 应该为市场提供流动性（当前市场制度是“正常”的）。

[彭博社](http://www.bloomberg.com/news/articles/2015-06-18/high-frequency-traders-first-go-against-order-flow-study-shows)

一项基于挪威主权财富基金交易行为的高频交易（HFT）行为研究报道指出，总体而言，HFT 算法是在为订单提供流动性，而非进行抢先交易（重点已加）：

> 根据包括挪威 8900 亿主权财富基金在内的投资者提供的交易数据，一项研究表明高频交易者更倾向于首先与大机构的订单流逆向操作。
> 
> ***研究发现，在第一个小时内，HFT“逆订单而行”，在多小时的交易中则转向顺应订单流***，由阿姆斯特丹大学教授文森特·范·克尔维尔和阿尔伯特·J·门克韦尔德于周四发布的研究显示。当 HFT 逆订单而行时，交易成本降低了 39%，“一个标准差”，而与他们同向交易时，成本则高出 64%，他们说道。
> 
> “这些结果与 HFT 在交易一开始就检测到大额、持久的订单并随之进行交易的情况是不一致的，”范·克尔维尔和门克韦尔德说。“我们推测 HFT 最终会感受到由此产生的不平衡。作为回应，他们理解到作为市场制造商，持有与这类订单相反的长期库存仓位是不利的。因此，HFT 更倾向于在一天结束时保持仓位中性。”

**尾部有多厚？**

另一种思考市场波动性的方法是查看股票回报是否具有厚尾。一个统计度量是峰度，其解释如下：

> 讨论了正态分布的形状之后，我们可以谈谈峰度和厚尾的含义。曲线下的总面积按定义等于 1。
> 
> 考虑到这一点，思考一下尾部更厚可能意味着什么。如果你想象一个有三个部分（都是假想的）的曲线——峰值、肩部（或中部），以及尾部，你可以想象一下如果将峰值拉高会发生什么。这会减少方差，并可能从肩部吸引‘质量’。但为了保持方差不变，尾部需要升高，增加方差，同时提供更厚的尾部。
> 
> 厚尾意味着尾部下的面积更大，这意味着其他地方必须减少——这意味着‘肩部’缩小，使峰值更高。为了比较两条曲线的峰度，两者必须具有相同的方差。冒着重复的风险，请注意方差对曲线形状有影响，即方差越大，曲线越分散。当我们说峰度仅在与其他具有相同方差的曲线比较时才相关，这意味着峰度衡量的是除了方差之外的其他东西。

![图片](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEic4W6sZNvrBvpXHhyphenhyphenDeBgocLbSumxGYRp8_R6X3nlGeDYHEvHcNVIe0yqtip7-PFkpqPcSrMeXYbS-omriEjXJf4IItGdUslYIkASAMvDHySDqBYdSOaPOnJnZryrgS4GLjx3-B8LCsRw/s1600/kurt_normal_vs_t.png)

对于非极客来说，以下是你们如何解释峰度。一个标准的正态分布的峰度为 0，而厚尾分布具有正的峰度。

这是自 1990 年以来每日标普 500 指数回报的滚动一年峰度图表。首先，中位数峰度为 1.34，表明股票回报的尾部比典型的正态分布更厚（使用基于正态分布的 Black-Scholes 模型的期权交易员对此非常了解）。此外，自 2011 年以来，峰度一直在下降，表明尾部正在变薄。这并不罕见，因为过去曾有过峰度甚至比今天还低的时候。

如果高频交易者进入市场，通过在微观层面买入低谷、卖出高峰来提供流动性，那么我们预计峰度会下降。

**高频交易（HFT）的巴丹死亡行军吗？**

从数据角度来看，认为高频交易算法是低波动性环境原因的假设很吸引人，但从商业角度来看却是非逻辑的。这是因为高频交易的盈利能力在过去几年一直在下降。这篇

[彭博社](http://www.bloomberg.com/bw/articles/2013-06-06/how-the-robots-lost-high-frequency-tradings-rise-and-fall)

2013 年（两年前）的文章展示了高频交易行业盈利能力如何逐年下降：

> 据 Rosenblatt 的数据，2009 年整个高频交易行业通过交易股票赚取了大约 50 亿美元。去年这个数字接近 10 亿美元。相比之下，摩根大通（JPM）在今年第一季度获得的利润是这个数字的六倍多。“利润已经崩溃了，”最大的高频交易公司之一，Tower Research Capital 的创始人 Mark Gorton 说。“容易的钱已经没了。我们现在做得比以前更好，但赚的钱却更少了。”
> 
> “交易的利润已经到了连很多公司的账单都支付不起的地步，”芝加哥大型公司 Chopper Trading 的创始人兼首席执行官 Raj Fernando 说，该公司运用高频交易策略。“现在肯定没人笑着跑去银行了。”过去一年，许多高频交易公司已经关闭。据 Fernando 说，很多公司在倒闭前都曾请求 Chopper 收购它们。他每次都拒绝了。

这张幻灯片来自一个

[高频交易展示](http://www.slideshare.net/jrapa/high-frequency-trading-overview-0529)

在 2014 年的讲述同样的事情（紫色批注是我加的）：

考虑到行业利润率这些年的下降以及 2013 年有关高频交易盈利能力下降的报告，行业进一步投入军备竞赛以降低波动性是不合逻辑的。这样的行为对高频交易来说等同于巴丹死亡行军。

根据这项分析，自 2011 年以来，高频交易算法可能有助于股票波动性的下降，但我不能得出它们是主要罪魁祸首的结论。股票市场波动性压缩的谜团依然是个谜。

<!--yml

分类：未分类

日期：2024-05-18 06:42:18

-->

# Pershing Square 和 IEX 上的信息泄露 | 机械市场

> 来源：[`mechanicalmarkets.wordpress.com/2016/01/03/pershing-square-information-leakage-on-iex/#0001-01-01`](https://mechanicalmarkets.wordpress.com/2016/01/03/pershing-square-information-leakage-on-iex/#0001-01-01)

Pershing Square 已经提交了一份更新的[13D](https://www.sec.gov/Archives/edgar/data/1336528/000119312515418565/0001193125-15-418565-index.htm)文件，披露他们上周卖出了 500 万股 Valeant。Pershing 几乎肯定认为这笔交易是敏感信息，但我认为他们的执行方法相当引人注目。

在我最近的一篇博客[文章](https://mechanicalmarkets.wordpress.com/2015/11/15/who-trades-on-which-dark-pools/)中，我提到一些机构流动可能会在 FINRA ATS[数据](https://ats.finra.org/)中留下签名。特别是 IEX 似乎有一些热情的客户，其中一些也是他们的股东。 [1] 除了 FINRA 数据外，IEX 还在其[网站](http://www.iextrading.com/tops/)上报告近乎实时的成交量数据，这可能会在交易完成之前很久就使客户流动变得可察觉。 [2] 我注意到，上一次 Pershing Square 交易 Valeant 普通股时，IEX 报告了那天的 Valeant 交易市场份额异常之高：

> 可能不仅仅是巧合，IEX 在 Pershing Square 最近买入 200 万股 VRX 时，其成交量占比异常之高。
> 
> 如果由于 Greenlight 或 Pershing Square 对 IEX 的支持而导致有价值的信息泄露，那么提及这种讽刺真是(几乎)太容易了。“Flash Boys”中 Ackman 对抢先交易的偏执占有重要位置。

所以，当 IEX 突然在[12 月 24 日](https://mechanicalmarkets.wordpress.com/wp-content/uploads/2016/01/iex_12-24_close.png)开始报告其在 Valeant 中的市场份额非常高时，这引起了我的兴趣。在又连续几天成交量持续走高之后，看起来非常可能 Pershing Square 在交易该股票。在 30 日，我[发推](https://twitter.com/mechmarkets/status/682221429824208896)了“我希望 Pershing Sq 读了我的帖子，”并附上了一些 IEX 上 Valeant 成交量的截图。

现在，IEX 有其他忠实的客户——例如，可能是 Greenlight 在交易 Valeant。但由于 Pershing 与该股票的密切关系，这种情况似乎不太可能。仅从肉眼观察[3]，当 IEX 在 Valeant 上有大量活动时，价格似乎要么下跌，要么保持稳定（有时会出现“锁定”现象）——而当 IEX 活动暂停时，价格往往会上涨。那种模式可能表明偏爱 IEX 的交易者在卖出。[4] 短期波动利润规则也意味着 Pershing Square 更可能卖出而非买入（参见[Matt Levine 的](http://www.bloombergview.com/articles/2015-11-24/bill-ackman-found-a-cheap-way-to-buy-more-valeant-stock)脚注 #5）。总的来说，当时的信息非常暗示 Pershing Square 正在卖出 Valeant 普通股。[5]

交易员总是与他们最喜欢的经纪人和市场中心保持关系。有时这些关系会导致执行质量不佳。但希望的是，交易员会因忠诚而获得其他好处。也许 Pershing Square 决定支持 IEX 的“亲投资者”议程是值得泄露他们的交易意图的。或者，更悲观的是，他们可能认为支持对 IEX 的投资更重要。无论如何，如果我是 Pershing Square，我会重新考虑这些决定。[6]

[1] IEX 首席执行官 Brad Katsuyama 透露，一些客户非常偏爱 IEX（在大约 [15m:10s](https://www.youtube.com/watch?v=AqKvJ-0LXe0) 的视频中）：

> 我们有一些非常紧密的合作伙伴，他们把很多交易都转向了 IEX —— 现在他们三成的交易量在我们的市场上执行。

[2] IEX 没有在其当前市场数据协议中报告交易或成交量。也许这说明 IEX 认为其交易数据是敏感的？不过，对机器来说，从网站上读取数据并不困难（像 [PhantomJS](http://phantomjs.org/) 这样的工具可能有用）。这些数据可能与合并磁带上的场外成交数据相匹配，以获得更精确的 IEX 交易视图。无论如何，如果 IEX 成为交易所，其交易将在磁带上明确标识。

[3] 显然，这远非严谨。我很想看到一项关于价格影响和 IEX 成交量大数据的分析。

[4] 流动性提供者显然知道他们在 IEX 上的对手是否有在特定分钟/小时/日/周购买或出售 Valeant 的倾向。我从未使用过这样的信息来做出交易决策（我的公司也没有），但我相信这样做是完全合规的。IEX 上 Valeant 的成交量（单独计数）与 Pershing Square [报告](https://www.sec.gov/Archives/edgar/data/885590/000119312515418565/d106380dex997.htm)的成交量相当。所以，如果 Pershing 将他们 1/3 的成交量发送到 IEX（见[1]），这意味着他们的订单流可能吸引了流动性到 IEX。其中很多可能是因为执行算法注意到了这一流动并选择与之互动。如果执行算法能利用暗池填充的信息来做出交易决策，那么量化交易者当然也可以。这可能比 IEX 声称要防止的信息泄露类型更重要。

[5] 当然，更大的情况可能会更加复杂。Pershing 可能在卖出普通股的同时，同时买入看涨期权或卖出看跌期权。

[6] 估算 Pershing Square 如果大力支持 IEX 可能获得的潜在好处的一些粗略方法：

1.  可能会有大约 500 万股在 IEX 上因此次（很可能）的路由决策而交易。按照每股 18 美分的价格，IEX 将能多赚 9000 美元。也许存在某种动量效应，即随着 IEX 接收更多的成交量，他们吸引未来的业务。那我们就宽容一些，说这个成交量对 IEX 及其项目来说价值 10 万美元，并且 Pershing Square 认为这个项目所有的好处都归机构交易者所有。

1.  或者，让我们假设 IEX 的“成功”意味着达到纳斯达克相同的市值，即 100 亿美元。500 万股大约是 IEX 每月 2-3 亿股成交量的 0.2%。假设 Pershing Square 通常每月交易一次，这样他们可以增加 IEX 长期收入的 0.2%。再次宽容地说，0.2%的营收增长可以提高 IEX“成功”的几率 1%。因此，Pershing Square 的忠诚度可以使 IEX 的预期价值增加多达 100 万美元。我很难解析 IEX 在其交易所申请中的[股本结构](https://www.sec.gov/rules/other/2015/investors-exchange-form-1-exhibits-g-n.pdf#page=29)，但让我们猜测 Pershing Square 拥有其中的 5%。这意味着 Pershing Square 将从他们路由偏好中收到 50 万美元的预期价值好处。

估算 Pershing Square 的成本：

1.  假设 Pershing 计划减少他们对 Valeant 的持股在完成交易前泄露了出去。Valeant 的股票会变动多少？我不知道，但保守估计至少应该是 1%吧？考虑到 IEX 上成交量的激增，市场会赋予 Pershing 正在出售的可能性多大的概率？我当时个人的估计是超过 50%，他们正在买入的可能性不到 10%（我和我的公司没有使用这些信息进行交易）。所以，也许由于这个泄露，股票会（确实）下跌 0.5%。如果 Pershing 还有 3 亿美元的交易资金，这个事件将使他们损失 1500 万美元。不难想象这个数字会更高几倍。

1.  假设 Pershing Square 想交易的不是 Valeant，而是一个大家都不预期他们会交易的股票。现在，看看 IEX 报告的成交量，人们可能对交易的哪一方，或者这笔交易是否来自 Pershing Square 了解不多。但是，IEX 上的做市商可能知道交易的一方。在 Pershing 的元订单开始交易后的第一个小时，也许这些高频交易者有 10%的把握猜测这个元订单很大（占日交易量的 50%）。让我们假设，正如 IEX 似乎认为的那样，高频交易者是残忍的，他们开始根据元订单预期的市场影响移动价格。使用平方根法则（例如[p8](https://workspace.imperial.ac.uk/quantitativefinance/Public/events/SLIDES%203RD%20IMPERIAL%20ETH/Jonathan%20Donier%20.pdf)），这个占日交易量 50%的元订单可能会预计将价格变动提高到股票日波动率的平方根乘以 0.5。假设日波动率为 1%，因此市场影响大约为 0.7%。然而，一个小时已经过去了，所以也许市场影响的一半已经发生。高频交易者有 10%的把握认为这进一步的 0.35%的变动会发生，所以他们将价格变动提高 0.03%。如果 Pershing 在这个时候还有 3 亿美元的交易资金，这 0.03%将使他们损失约 100 万美元。也许 Pershing 每年会交易这个规模五次，所以路由偏好可能使他们每年损失 500 万美元。这是对高频交易订单预期的偏执（且粗略）估计，但偏执似乎是 IEX 企业文化的组成部分。

无论如何，在我看来，Pershing Square 偏袒 IEX 的成本似乎超过了慷慨计算的好处。但我猜想，这里的几百万可能对他们来说不是什么大问题。

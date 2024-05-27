<!--yml

类别：未分类

日期：2024-05-18 16:50:37

-->

# VIX 和更多：读者 Q 和 A：straddles 和隐含波动率

> 来源：[`vixandmore.blogspot.com/2011/04/reader-q-and-straddles-and-implied.html#0001-01-01`](http://vixandmore.blogspot.com/2011/04/reader-q-and-straddles-and-implied.html#0001-01-01)
> 
> *在上周三收盘前，我放置了一个 ATM straddle，证明是盈利的，我在周四 IV 波动后平仓了。我不应该再来一次，但在周二价格大幅下跌后，IV 崩溃只让我勉强持平。这是我第一次做两个超短期波动交易，现在我知道 CBOE 网站上的免费 IV 数据是一个日终服务...绝对不会在周一下午放置那个交易。现在我知道我可能应该反向操作，做空波动率，你建议任何不是纯粹做空且不需要大量保证金的战略吗？*
> 
> *另外，你用什么服务来查看 ETF 等实时的 IV？*
> 
> *Adam C.*

Hi Adam，

作为一名新手，你应该区分那些有无限风险的期权交易和那些你可以将其特征为有限风险或定义风险的交易。卖出 10

[SLV](http://vixandmore.blogspot.com/search/label/SLV)

7 月 47 美元看涨期权理论上会使你面临无限风险，因为 SLV 可能会继续上涨。如果这种情况发生，取决于你的现金缓冲，最终你的经纪人会给你发出保证金追缴通知，你将被迫在重大损失的情况下平仓。

采取同样的基本交易，再增加一个对冲的第二腿，你的无限风险现在变成了有限风险。而不是裸卖空，涉及 10 份 SLV 7 月 47 美元看跌期权和 10 份 SLV 7 月 50 美元看涨期权的熊市看涨期权价差将你的损失限制在两个执行价格之间的距离。现在是 50-47，即三点。三倍 10 份期权（乘数 100）将你的最大损失定为 3000 美元。

立即进行这笔交易，对于 10 份合约，你应该会收到大约 1.20 美元的信用，这意味着你的最大利润是 1200 美元，最大损失是 3000 美元-1200 美元，即 1800 美元。

这是一个方向性赌注。对于一个非方向性赌注——意味着你预期 SLV 在 7 月份到期时大约为 47.00，你应该专注于

[condors](http://vixandmore.blogspot.com/search/label/condor)

以及

[butterflies](http://vixandmore.blogspot.com/search/label/butterfly)

，这实际上是

[strangles](http://vixandmore.blogspot.com/search/label/strangle)

以及

[straddles](http://vixandmore.blogspot.com/search/label/straddle)

。有时你可能会听到交易员提到“购买翅膀”。这意味着他们通过购买虚值期权来对冲风险，将无限风险的宽跨式或海龟策略转换为有限风险的铁鹰或蝴蝶策略，正如上面提到的看涨期权价差例子一样。实际上，一种思考铁鹰策略的方式就是它只是一个

[熊市看涨期权价差](http://vixandmore.blogspot.com/search/label/bear%20call%20spread)

加上一个

[牛市看跌期权价差](http://vixandmore.blogspot.com/search/label/bull%20put%20spread)

。早期我使用了一个更通用的标签

垂直信用价差](http://vixandmore.blogspot.com/search/label/vertical%20credit%20spread)

对这些策略的博客。你应该能够通过这些链接获取更多信息。

了解这些策略的更好方法是利用一些在线资源。一个不错的起点是期权行业委员会（OIC），在那里他们有一个

[期权策略指数](http://www.optionseducation.org/strategy/strategy_index.jsp)

。点击任何策略图表以获取更多信息。在众多优秀资源中，我强烈推荐

[CBOE 期权研究所](http://www.cboe.com/LearnCenter/default.aspx)

，你可能想从他们的

[教程](http://www.cboe.com/LearnCenter/Tutorials.aspx)

。请注意，期权经纪商也在很好地教育他们的客户关于期权策略。在教育方面投入很大努力的两个经纪商是 optionsXpress (

[教育中心](http://www.optionsxpress.com/free_education/education_center.aspx)

和 thinkorswim (

[游泳课程](https://www.thinkorswim.com/tos/displayPage.tos?webpage=trainingProducts)

。

此外，下面的链接应该提供一些具体的帖子，这将为你提供关于你最近 SLV (?) 交易的一些思考和一些替代方法。

在实时 IV 方面，我使用

[Livevol Pro](http://www.livevol.com/livevol_pro.html)

，它提供了我在博客上使用的图表

[隐含波动率](http://vixandmore.blogspot.com/search/label/implied%20volatility)

和

[历史波动率](http://vixandmore.blogspot.com/search/label/historical%20volatility)

开始。你最喜欢的期权经纪商（thinkorswim, optionsXpress, TradeMONSTER, Options House, Trade King 等）也应该有好的实时或接近实时的 IV 数据。如果你没有在专门从事期权的经纪商处开设账户，我强烈建议你至少在上面提到的经纪商之一开设一个账户，这样你可以在同一个平台上获取数据和进行交易。

相关帖子：

***披露(s):*** 写作时持有 SLV 空头；Livevol, CBOE, optionsXpress, TradeMONSTER, Options House 和 Trade King 是 VIX 和 More 的广告商*

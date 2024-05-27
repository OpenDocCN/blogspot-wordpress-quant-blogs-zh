<!--yml

分类：未分类

日期：2024-05-18 06:43:36

-->

# 萨拉奥操纵指控与队列位置 | 机械市场

> 来源：[`mechanicalmarkets.wordpress.com/2015/04/24/sarao-spoofing-allegations-and-queue-position/#0001-01-01`](https://mechanicalmarkets.wordpress.com/2015/04/24/sarao-spoofing-allegations-and-queue-position/#0001-01-01)

关于萨拉奥案许多未回答的问题之一是，他是否能够合理地辩称，他所谓的“欺诈”订单实际上是市场制造策略的一部分。布拉德利·霍普（Bradley Hope）[上传](https://twitter.com/bradleyhope/status/591375301537570817)了一些文件，我认为这些文件可能有助于回答这个问题。

美国联邦调查局（FBI）的投诉书（[点击查看](http://www.justice.gov/sites/default/files/opa/press-releases/attachments/2015/04/21/sarao_criminal_complaint.pdf)）提到了萨拉奥如何经常修改他的订单，但没有太多关于这些修改性质的详细信息。频繁修改订单本身并不一定意味着操纵行为。市场制造商使用该交易所指令更新他们的报价有很多合法理由。也许萨拉奥的辩护可以提出他实际上意在市场制造，只是离最佳买卖价（BBO）几个点而已。他肯定不是唯一一个在当前价格远端发布流动性的市场制造商，这种交易策略可能是存在已久的策略之一。如果是这样，那么高修改率和低成交率将保持一致。也许他可以声称他倾向于在卖出侧发布更多数量，这是他报价策略的一部分（记住，他似乎主要在波动时期交易）。

所以，我想知道的一个细节是，萨拉奥是否用这些修改请求来更新合法的报价，随着市场价格的变动，或者他是否用它们以其他更倾向于操纵的方式。昨晚的文件可能包含暗示。从第 53 页开始，包含萨拉奥致交易技术公司（Trading Technologies）的电子邮件：

> 我需要的功能如下…
> 
> iv) 我的订单能够停留在特定数量上，即如果没有 x 个订单在我之下，我的订单将被取消。当然，为了使这正常工作，我们必须待在订单簿的最后，v) 这可以通过每次检测到新的订单时，我的订单增加/减少 1 个数量来实现

这可以帮助解释他所谓的高修改率，在我看来，这真的很奇怪。如果我理解正确（也许我理解不对），他要求一个自动向交易所发送 2 个修改请求的功能，每当有人加入他的价格水平时。第一个请求将增加他订单的数量 1 个单位，紧接着，第二个请求将减少它 1 个单位。这将导致他的订单数量没有净变化，但将有助于把他移到[FIFO 队列](http://www.cmegroup.com/confluence/display/EPICSANDBOX/Matching+Algorithms#MatchingAlgorithms-FIFO)的后面。队列末尾的订单只有在整个价格水平交易时才会被填充，这通常表示一个非常有毒的 incoming order。

为什么有人想要他们的订单在队伍的后面，这几乎肯定比前面有更差的逆向选择特征呢？[一种可能性](https://twitter.com/garybasin/status/591400826574344192)是，他想站在队伍后面，让他的策略提前知道被扫过的价格水平，因为交易确认有时会[发送给在公开数据馈送分发之前执行的人](http://www.wsj.com/articles/SB10001424127887323798104578455032466082920)。然而，这样做大型订单没有意义，这也不符合我们对 Sarao 是一个低速交易者的看法。[另一种可能性](https://twitter.com/patrickrooney/status/591407223747796993)是，他想降低他的填充率，以避免在多个产品上同时被填充，但仍报价大量规模。我对这样做是否会提高策略的盈利性有些怀疑。但我对许多市场都不熟悉，也许在某些市场上，对于资本受限的交易者来说这是有意义的。

但是还有第三种可能性：他想站在队伍的后面，以最小化自己的交易机会，而不管交易的实际盈利性。这与这些所谓订单旨在完全欺骗他人的假设相一致。支持这一假设的另一个线索包含在他发给 FCA 的 Joanna Jasina 的一封电子邮件中（同一文件的 p48）：

> 难怪他们[HFTs]可以 manipulative on top of my orders without any risk, for even when I change my mind and decide to sell into my buy order, the manipulative orders on top of my initial buy order disappear in the 4 milliseconds it takes for my buy order to be cancelled and replaced with my sell order so that I do not trade with myself !!!!!!

这句话表明，当他取消了他的订单时，队列中排在后面的人很快也取消了他们的订单。假设萨拉奥确实在虚造订单，这可能意味着他有时希望与那些复制他的“虚造”订单的人交易。为了不与自己交易，他要么必须在尝试与受害者交易之前删除自己的订单（显然是能够迅速响应并删除的高速度交易员），要么他必须排在受害者的订单之后。我对 CME 对自我交易的态度印象不佳，这还是在[自我匹配预防](https://mechanicalmarkets.wordpress.com/2015/03/31/manipulation-using-compliance-tools-equities-analysis-inspired-by-allston-case/)出现之前，所以，如果萨拉奥坚持这种虚造订单的方式，他只能把他的订单发送到队列的末尾。

这种讨论都是假设性的，我不确定这些电子邮件实际上是否反映了他当时的想法，但我想听一听调查人员关于萨拉奥交易活动的确切细节。

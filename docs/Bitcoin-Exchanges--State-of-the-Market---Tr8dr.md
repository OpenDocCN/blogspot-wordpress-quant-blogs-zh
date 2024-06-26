<!--yml

类别：未分类

日期：2024-05-18 15:28:30

-->

# 比特币交易所：市场现状 | Tr8dr

> 来源：[`tr8dr.wordpress.com/2015/02/08/bitcoin-exchanges-state-of-the-market/#0001-01-01`](https://tr8dr.wordpress.com/2015/02/08/bitcoin-exchanges-state-of-the-market/#0001-01-01)

在之前的帖子中，我概述了将为前 4-5 个比特币交易所准备高质量的 L2/L3 数据源，收集 L3 数据，并提供用于交易的合并实时订单簿的意图。 目前已经实现了 OKCoin，并且一直在尝试其他交易所以确定它们的 API 能力。

除了 OKCoin 外，到目前为止我发现的情况都不太好。 以下是关于市场数据 API 的前 4 个交易所的摘要（我还包括了 Coinbase，并认为它将成为一家主要参与者）：

![Screen Shot 2015-02-08 at 9.33.28 AM](https://tr8dr.wordpress.com/wp-content/uploads/2015/02/screen-shot-2015-02-08-at-9-33-28-am.png)

**BTCChina** 显然是最大的交易所，但是技术似乎有问题（至少在市场数据方面是这样）。 他们在去年 11 月实现了 FIX 4.4，但是存在问题，因为对完整订单簿的请求未按文档执行（如果有人在此方面取得了成功，请告诉我）。 BTCChina 还有另一种公共 WebSocket/JSON API，提供了仅有 5 个订单簿级别。 然而，似乎有一种“秘密”API 提供了完整的订单簿深度，因为实时 UI（如 bitcoinwisdom）显示了超过 5 个级别的活动（如果有人知道这是如何实现的，请告诉我）。 **附录**：我已经联系了 BTCChina，希望他们能解决 FIX 订单簿订阅问题，并不将其视为一个功能。

**OKCoin** 是按成交量计算第二大交易所，并且似乎有最活跃的订单簿。 好消息是，它的 FIX API 按文档执行。 在活动方面，每 100-300ms 或平均 15ms 之间都会收到 20+ 笔交易。 这种活动程度可以与更传统的市场相媲美。 也就是说，我怀疑交易所或市场做市商（交易费为 0）正在不断地在订单簿的前 3-5 个级别的两侧不断抬高市场。 我看到的模式是，市场的两侧都有非常浅的订单（1/10 BTC），这些订单会交替地在两侧被清除。

**Bitfinex** 似乎是最受欢迎的 BTC/USD 交易所，因此即使存在不明智的市场数据 API，也不能忽视。 他们正在进行 AlphaPoint 的“现代”交易所实现的 beta 测试。 一旦上线，应该会提供 FIX 和二进制流数据。 我不知道这些是否会提供交易所的 L2（订单深度）或 L3（订单交易）视图。 无论哪种都将受到极大欢迎。

**BitStamp** 在其 BTC/USD 交易量份额方面急剧下降。 鉴于其困境，我想知道它是否能够生存下去。 尽管它有一个提供 L3 数据的“秘密”API，但支持交易所的技术值得怀疑。 特别是，其撮合引擎既存在[不正确的撮合语义](http://www.reddit.com/r/Bitcoin/comments/1r4d6t/bitstamps_streaming_api_and_exploitation/ "不正确的撮合语义")（在 Reddit 上有文档记录），而且**非常缓慢**，扫描几个层级可能需要几秒钟才能执行。 除非 Bitstamp 在技术和信任方面彻底改革自己，否则问题是，谁将取代它成为 BTC/USD 市场上的第二大存在？

**Coinbase** 或者尚未推出的 Gemini，可能会在市场地位上取代 Bitstamp（甚至可能超越 Bitfinex）。就市场数据而言，它提供了订单簿中所有订单的完整列表。 **更新**：Coinbase 有流式 API & 具有第三级数据，我的错误。 ~~但是这必须通过轮询他们的 REST/json API 来查询。 您可以想象，这不是一种可扩展的方法——订单数量将随着时间的推移而增长，到达一定程度时，消息大小将周期性地变得不堪重负。 正确的解决方案是具有订单事务“增量”的流式 API {新订单，删除订单，更新订单等}。 最基本的设计、规模和可访问性错误已经反复出现，在一个备受关注的交易所启动过程中（受监管的、纽交所支持的等）。~~

**中国交易所**

关于中国交易所的成交量和可成交性，很难辨别什么是真实的。 我没有与 OKCoin 或 BTCChina 任何交易经验，然而，从多个来源（[例如](http://www.reddit.com/r/BitcoinMarkets/comments/2swttr/okcoin_unusable_during_this_drop/ "例如")）已经注意到以下情况：

+   OKCoin：在价格大幅波动期间，交易所不响应交叉订单（价格波动时遭遇的 DDOS 攻击）

+   OKCoin & BTCChina：大规模洗盘交易和垃圾订单（显然是交易所自动交易机器人，否则就不经济）。 这与我在 OKCoin 的市场数据中看到的情况相吻合。

至少作为数据来源，我认为这些交易所提供了价值。 更理想的情况是找到一种方法用于交易，并避免无法执行的情况。 关于在更大的价格波动中无响应的交叉订单，问题是这是否是由于较差的撮合引擎技术（订单簿可能被压垮）[1] 还是故意为之“为了交易所自身”的[2]。 看起来交易所很可能除了提供交易所服务外，还在自己的名义进行交易。

今天也有坏消息，一个总部位于香港的交易所（MaiCoin）[消失了](http://headlines.yahoo.co.jp/hl?a=20150208-00000055-jij-cn "消失了") ，客户存款价值 30 亿港元。我认为比特币领域存在足够的欺诈和糟糕的市场惯例，某种程度的监管和受监管的交易所将受到欢迎。

**结论（技术）**

我对（大多数）交易所比特币技术的总体印象是，它是由典型的全栈 web 应用程序开发人员设计的，几乎没有从传统市场中获得任何经验，也没有在规模上应用常识。在比特币交易所中，使用 REST/JSON 轮询是最愚蠢的想法之一（尽管对某些用途来说是可以的）。对于这种外部接口/设计决策，人们不得不想知道幕后还有什么其他奇迹。

我相信这些会成熟，并通过竞争，会趋于更加复杂和合理的设计。如果没有其他原因，我将乐意与这些交易所协商，将它们的 API 和实现移向最先进的状态，以使其成为更好的交易场所。

**注**

[1] 鉴于在 BTC 领域看到的无知/轻率的实现，大多数交易所如果在订单量扩展方面具有不足，也就不足为奇了。当然，Bitstamp 确实有这个问题。

[2] “为了房子”的骗局是故意延迟和提前运行的：在市场上涨期间，延迟购买流量，提前购买买家流量，并以更高的价格将其卖给潜在的买家。

<!--yml

类别: 未分类

日期: 2024-05-12 19:55:59

-->

# Falkenblog: Uniswap V2 Made Money. What Happened?

> 来源：[`falkenblog.blogspot.com/2024/02/uniswap-v2-made-money-what-happened.html#0001-01-01`](http://falkenblog.blogspot.com/2024/02/uniswap-v2-made-money-what-happened.html#0001-01-01)

我惊奇地看到了[一条推特](https://twitter.com/AnthonyLeeZhang/status/1753563488062935252)，@AnthonyLeeZhang 在其中提到了一篇短文，展示了在 Uniswap 的 ETH-USDC 池中，流动性提供者（LPs）赚到了钱，而我[曾指出](https://efalken.substack.com/p/video-on-how-to-calculate-amm-lp)自 Uniswap 开始以来 LPs 已经一直在亏钱。我最初以为这是一个错误，但发现他的盈亏指标最终和我是一致的。

具体来说，他使用[Milionis, Moallemi, Roughgarden, and Zhang](https://arxiv.org/abs/2208.06046)的盈亏表述，他们称之为 Hedged LP PnL。这是做市商在考虑**无常损失**（*又称*，重新平衡损失**，LvR**，**凸性成本**）后的盈利。

> 被对冲的 LP 的盈利 = 手续费 - LvR = Vt - V(t-1) - mints + burns + hedgePnL

在这里，V(t)是池子储备的价值。如果我们使用 ETH-USDC 池，其中 p(t)是 ETH 价格等于 USDC 的数量，我们得到

> V(t) = USDC(t) + ETH(t)*p(t)
> 
> V(t-1) = USDC(t-1) + ETH(t-1)*p(t-1)

储备价值的差异受到价格变动以及由铸造（LP 存款）、销毁（LP 取款）、交易和手续费引起的 USDC 和 ETH 的变化。流入池内的 ETH 和 USDC 既包括手续费，也包括交易者出售的代币（交换成了池中的代币），这意味着

> USDC(t)=USDC(t-1) + mints(t, t-1) - burn(t, t-1) + NetUsdcIn(t, t-1)
> 
> ETH(t) = ETH(t-1) + mints(t, t-1) + burns(t, t-1) + NetEthIn(t, t-1)

[注意：(t, t-1) 是 t-1 到 t 期间的流血]/。这可以简化为仅仅根据交易者交换事件日志中记录的池子的 net USDC 和 ETH 的价值来确定，在期末计算价值。当进行铸造和销毁时，忽略价格会产生一些差异，但两种方法都做出了这些 PnL 的近似计算，差异并不大。我更偏爱这样的公式，因为它需要的数据更少。

> 被对冲的 LP 盈利 = NetUsdcIn(t, t-1) + NetEthIn(t, t-1)*p(t)

虽然可以使用任意期限的时间段作统计，但从极限上来看，这并不重要。作为实际考量，以日历日拉取数据非常适用于观察趋势，并且可以避免交易成本，如果有人实际上对他们的 LP 池头寸进行对冲操作。

更重要的是，这使我了解到 Uniswap 的 v2 版本，这款旧的资产效率低下的自动做市商（AMM），为其提供流动性提供者（LPs）创造了收益。我最初认为这无疑是以各个方面都逊色的存在，这就是为什么它标志性的 ETH-USDC 30bp 费用（基点，0.3%）的池子的交易量仅为 ETH-USDC 5bp v3 池子的 2%，后者大约是不受欢迎的 30bp v3 池子的一半。

| ![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEicYCQ_o9LLMbSP_k473zDd_RAuYhq-x225B-VoqHDhv3dikQd7Am-C8Z_jZy58OeOlcF1qRhKYbmKZnNltgYxQXf1s-Gv7rUSeAN-4js_t9CLFX0hSNudWQNogGOpdiNIl1gCKaNf3DTO8ZNT8mIkAFPut-42oMo5K6R0MOR9CkmPdVRefir4jJA/s692/v2v3volume.png) |
| --- |
| ETH-USDC 池 |

Uniswap 的 v2 于 2020 年 5 月开始，当 Uniswap 升级的 v3 池在 2021 年 5 月开始时，交易量达到了顶峰。不仅他们的 v2 LP 在过去赚了钱，而且他们一直在从 LP 获利至今。在其首年 2020 年，Uniswap 的 v2 池每天为池子赚取超过 10 万美元，每年总计为池中锁定的资产价值带来甜美的 30% 以上的年收益率（考虑了无常损失/LvR/凸度成本）。

| ![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjyukdKVPc3_YRIQbEgVrUeBqwjnLuPiUPsNq5sXiU8tFLGcicRR8l8Pa7RUgzOx2lJT8LGyk6d1F7uytfPMqYSA6kLUXbb-Y9sl07lDHoFhz1VEb1bXok7TH5JyZMALqg6o9sLckJmQbPFzZQ6T9w5KHc7ivnzVzGZwLmja847ODBeyKuIE0ScIA/s680/uniprof.png) |
| --- |
| Uniswap v2 ETH-USDC 池 |

目前，ETH-USDC v2 池中大约价值 100 百万美元的代币，并且它产生了适度但仍然是正的 3% 年化收益率。就 PnL/USD 交易而言，它表现得更加令人印象深刻，展现了稳定的盈利能力（见下文）。相比之下，v3 池从一开始就亏钱。虽然 v3 LP 盈利的日子是亏损日子的两倍，但卖出 gamma（具有负凸度）的问题在于，一旦出现亏损，亏损额相对较大。不幸的是，这导致很多骗子和愚人认为他们只需要更好地把握时机或份额大小。

| ![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEio1eoaO7P3aHsIViCDTcXKYMUDrdxpbH8eXix4XRuBFtKhjsKPyge1A79bpLN5euux9eJ2B7mJwkGzO_zeh8r3HS938lw04ZlVYs5nVP25QyU9iXc6NuRfRtOZNiFnmQqxRFJdvFcs6_JCpe9htaJ35F5FenDRZdLYNVWMs8e4W5jKq5tkcic1eg/s670/pnlusd.png) |
| --- |
| ETH-USDC 池 |

这是一个非常有趣的平衡。30bp 费用的 v3 池对应于 30bp 费用的 v2 池，然而 v3 LP 亏钱而 v2 LP 赚钱。问题在于，相对于总交易量，v3 池的流动性过大。如果池子接近 Binance 等交易所上反映的“真实”价格，标准波动意味着一定程度的交易量。具体来说，在短时间内，价格的百分变动与相对于流动性的交易量相关。请记住，在 AMM 中，流动性定义为

> 流动性 = sqrt(池中的 USDC * 池中的 ETH)

应用 AMM 数学，我们得到

> 返回率% = 2 * DUSDC/(流动性 * sqrt(p))

如果我们将日波动率设为 5%，那么每五分钟的标准差就为 0.3%。如果套利者平均每五分钟将价格推高 0.3%，那就需要实现总共 85% 的价格变化。这意味着套利或定价交易的金额是流动性的线性函数。

> DUSDC(来源于套利交易) = 0.85 * 流动性 * sqrt(p) / 2

如果 LP 需要一定比例的流动性交易者相对于套利交易者，那么如果（USDC 交易量/流动性）比具有相同费用的池低，它将赚取更少的钱，甚至赔钱。5bp 池至少需要每单位流动性交易的 USDC 交易量高出 6 倍。

我们看到，对于 v3 的 5bp 池，成交量/流动性比 v2 池高出 2.5 倍，远远低于需要的 6 倍。在 v3 的 30bp 池中，这个比例约为 v2 池的 50%。旗舰区块链上的旗舰 dapp 的旗舰 AMM 一直是一个失败者，目前仍然如此。对于 AMM 来说，这是一个存在问题，因为大用户被限制在没有可持续的流动性 AMM 的中心化交易所。这些中心化交易所是必要的，但如果加密货币要避免外部机构对主要法定货币的攻击，它们不能成为大宗交易的必要条件。

| ![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhqMNwSJ4Ed6KAWU1AjY-idwMEhgj77hUn-a1d-Vq_278EL02C3tAcUNz5OvZWCRmAUPFgi_PXP8IDI_0tPJquywwpJC1t7wEKuOz628u94wV7z3VQDPfoLPegmD8JN1YWHoVZFq8vpVBz0swOkM6NEvECA3PI55vWZcA8IkRhY7HAiGDwBRBC6aA/s669/volliq.png) |
| --- |
| ETH-USDC 池 |

相对于 v2 的 AMM，我只能推测 v3 发生巨大失败的原因。我怀疑原因是 LP 没有意识到 LP 的凸性成本。如果你在 Reddit 的 Uniswap 主题中浏览，你会看到偶尔有人询问如何衡量或对冲 LP 的负凸性，而且讨论的内容类似于大学生讨论宏观经济问题时的强烈、无知的观点。大多数人甚至没有意识到凸性成本。那些意识到的人认为可以通过审慎的时机、更低的延迟或解决鸡和蛋问题的奖励计划来克服这个问题。还有一些人认为解决办法是购买波动性作为对冲，而在区块链的背景下，这不仅资本效率低下（你无法实现交叉抵押），而且如果你在中心化交易所上以比实际波动性更低的价格出售波动性，对冲就只会锁定你的损失。

使用 v2 池时，LP 都会感到一种共同的成本：资本。每个 LP 都根据他们在 AMM 池中的股权按比例对待。相反，许多 v3 LP 认为，他们通过集中他们的流动性在一个狭窄的范围或根据当前的波动性调整他们的范围，可以超越其他 LP。他们从未考虑过额外流动性的影响。最终的结果是持续的过剩流动性，这不仅会稀释利润，而且会使其变成损失。流动性越大，凸性成本就越大，这与仅仅增加股票份额不同，它会影响净收入的符号。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgP6ETiogihmrUxWFv91uyHN8omwvHgODpTtTv9deSH4Jca3Xey-GAzNDkN-Ic1DxC5Z_aCz-zaCQd_15I4zgEzTwYpVcM1PrZ7oCDsFmt-dROpVfFSK2q8WpouwtbczZAh9mQxioVRfzsRH_J-UM0zO9hS7D_11bHLNxHsCfUvrU-0F8jzOhkesQ/s648/v2capital.png)

许多人已经写过，将资金添加到 v3 池显然比为 v2 池提供流动性更好，因为通过将范围限制在慷慨的上下 20%，他们只需使用总资本的 8%就能部署相同金额的流动性。他们从未考虑如果每个人都得出相同的结论会带来什么后果，导致流动性过剩与池的凸性成本线性相关。由于大多数人不理解，更不用说衡量凸性成本，他们毫不在意地将资本存入这些池中，忽视了这些成本对底线的影响。

不幸的是，我的垃圾邮件文件夹里充斥着在 20 世纪 90 年代就是陈词滥调的同样骗局。然而，虽然阳具增大药丸行业非常固执，但并没有增长。要使区块链上的合约能够运作，它必须超越类似通过代币奖励（这只是稀释 LP 费用）或无限使用抵押代币作为抵押品的杠杆这样的花招。不幸的是，2021 年获得巨额利润并且避免被起诉或破产的投资者——可能纯属运气——是指导我们当前发展的主要风险投资者。他们有很多不想报告的资金，而且其他事情也是无所事事。他们知道一些术语，但尤其是对伽马或一般机制设计一无所知。

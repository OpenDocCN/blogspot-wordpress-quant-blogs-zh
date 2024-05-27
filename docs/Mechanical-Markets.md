<!--yml

分类：未分类

日期：2024-05-18 06:45:01

-->

# 机械市场

> 来源：[`mechanicalmarkets.wordpress.com#0001-01-01`](https://mechanicalmarkets.wordpress.com#0001-01-01)

经济学中的一个核心挑战是理解价格如何影响供需量，这种关系通常被假设为大约是线性的。但是，有些市场中这种线性的观念，有时被称为“弹性”，可能不成立。在一份[论文](https://arxiv.org/abs/1506.03758)中，Donier 和 Bouchaud 展示迅速清算市场（具有布朗运动价格过程）的供需曲线平均形状是局部的二次的，没有线性项。

以下是总供给和需求随价格变化而变化的经典说明：

![img/8d259d0fa3d5b121503e818163009706.png](https://mechanicalmarkets.wordpress.com/wp-content/uploads/2017/04/sd_curve11.png)

总需求随价格下降而减少——总供给随价格上升而增加。曲线在![p*](img/fc13cdcdcef4fb20d1b4cedc27f9111b.png)处相交，这是体积最大化的市场价格。 [1] 在市场价格附近，供给和需求随价格变化而线性变化。

如果我们“清算”市场，使得在![p^*](img/c4c67bb2dfe7cbed69d3a33c322ed3e7.png)处的供应与在![p^*](img/c4c67bb2dfe7cbed69d3a33c322ed3e7.png)处的需求相交易，那么曲线将看起来像：

![img/a8a64acc74285e38647c4de405826042.png](https://mechanicalmarkets.wordpress.com/wp-content/uploads/2017/04/sd_curve2-svg.png)

这与第一个图表相同，只是向下移动了交易量。曲线在![p*](img/fc13cdcdcef4fb20d1b4cedc27f9111b.png)附近仍然是线性的。如果我们放大，平均供需曲线将看起来像 [2]:

![img/b2b60f4520c6f1e88cd002b2db1ff7aa.png](https://mechanicalmarkets.wordpress.com/wp-content/uploads/2017/04/sd_curve3-svg.png)

但是，Donier 和 Bouchaud [3] 表明，具有某些特征的市场实际上将具有局部的二次平均供需曲线。即：

![img/9c17aa640e0a161673d3c6032fc49c4a.png](https://mechanicalmarkets.wordpress.com/wp-content/uploads/2017/04/sd_curve4-svg.png)

在这个阶段，一个市场订单的价格影响将与其大小的平方根成比例，平均而言。

他们的结果也引发了这样一个问题：一些市场是否在其生产和消费曲线的鞍点处运作，这可能看起来像：

![img/89a0cbcfce62ff0da6fc0bad51834044.png](https://mechanicalmarkets.wordpress.com/wp-content/uploads/2017/04/production-demandrate-svg.png)

其中![W_{saddle}](img/97077e998cba6de830f16cfd9bda6709.png)是“鞍区”的粗糙宽度，曲线主要是二次的区域。

这让我觉得与经典经济画面有质的区别。这也直观地讲得通：当一个资产波动大时，很难确切知道供求平衡的价格。唐耶尔和布绍 aud 没有推测![W_{saddle}](img/97077e998cba6de830f16cfd9bda6709.png)的大小，但至少有可能他们的结果适用于比预期更广泛的价格范围。如果任何实际市场有一个大的![W_{saddle}](img/97077e998cba6de830f16cfd9bda6709.png)，估计其价格弹性将是困难的或不可能的。这也可能解释金融市场的冷漠——在那里，产生头条的价格变动对实际世界的供求没有多大影响。 [4]

# 唐耶尔-布绍 aud 模型

唐耶尔和布绍 aud（以及之前的合作者）使用了一个反应-扩散模型来得出这个结果。简单来说：

1.  以概率![\omega_+(y)](img/e462d03dffed871fccea6e29088b6d5d.png)在时间间隔![dt](img/a1ecf7a8e1caa9fec2ff0bb7108ad361.png)创建新的买入订单，其中![y = p - p^*](img/25f0361152a995227d96d50d61e6adf3.png)是新订单价格(![p](img/daecc39de4dc7417beb137da548b5756.png))与市场价格(![p^*](img/c4c67bb2dfe7cbed69d3a33c322ed3e7.png))之间的差。卖出订单以概率![\omega_-(y)](img/1851b93670d0be32312ec74798a3a40e.png)创建。

1.  现有订单以概率![\nu_{\pm}(y)](img/d758b5468d0662c8c8a0496fadec31c7.png)取消。

1.  市场在每个周期时间间隔![\tau](img/cd658e7d265e9e2b16272c4001abe15f.png)时清除——当买入和卖出订单的价格相交时，从市场中匹配并移除。

1.  价格![p^*](img/c4c67bb2dfe7cbed69d3a33c322ed3e7.png)的基础过程是布朗运动。

当![\tau](img/cd658e7d265e9e2b16272c4001abe15f.png)很小时，他们显示供求曲线在局部是二次的，对于任何合理的![\omega_{\pm}(y)](img/39b05154c0f9dcee82f5e4a5e4133f61.png)和![\nu_{\pm}(y)](img/d758b5468d0662c8c8a0496fadec31c7.png)。

当然，现实世界的市场并不会立即清除交叉的元订单，即使市场在连续时间内交易。例如：一个交易者可能打算以任何低于$100/股的价格购买 1 亿美元的股票，而另一个交易者则打算以任何高于$90/股的价格出售 1 亿美元的股票。这两个交易者可能会在几周内逐渐发出他们的订单流，而不是立即以$90 至$100 每股的价格相互交易。 [5]

尽管如此，可以想象一些市场的行为仿佛它们处于小的![\tau](img/cd658e7d265e9e2b16272c4001abe15f.png)极限。在比特币市场，交易者可能不像在传统市场那样倾向于隐藏他们的意图，并且可见订单簿可能代表市场价格附近的真实供需水平。作者在[图 6](https://arxiv.org/abs/1506.03758)中展示了比特币的平均显示供需，这与结算价格 2%内的价格的累计供需（通常累积供需约为 400k BTC）非常接近一个二次函数。所以电子市场的“马鞍区”可能与它们的日波动性一样宽，这并不令人惊讶；很少有石油生产商因为价格上涨 1%而增加钻探。

# 潜在流动性作为首次穿越时间

唐尼和布肖的结果似乎是布朗运动价格过程的一般特征，并不依赖于模型的具体细节。他们模型的精神提出了一个问题：在给定价格的边际供给/需求之间，是否存在联系，以及市场穿越该价格所需的时间。也就是说，潜在流动性是否具有与首次穿越时间统计类似的性质。

二次供给/需求曲线等价于边际供给/需求随价格线性变化。根据定义，在价格![y](img/4d2c4d231bb45c490a6d88946970f81f.png)远离“真实”价格的累积供给(![S(y)](img/d77cad39370403c182cce0cbfbf4375c.png))只是截至该价格的边际供给(![\rho_{S}](img/d8df4abe198dbd354542c839c026f52a.png))的总和：![S(y) = \int_{0}^{y} \rho_{S}(y') dy'](img/d59eb9511727548523c3c51a75182f57.png)。6 ![\rho_{S}(y)](img/04ad9e017f228e019ce53abe6c7516a1.png)也可能被称为在价格![y](img/4d2c4d231bb45c490a6d88946970f81f.png)可用的隐性卖出订单的体积。

达到唐尼（Donier）和布肖（Bouchaud）的结果的一种方式是假设![\rho_{S}(p)](img/02e0a4f75b678b31dcd56098fa8b5435.png)随时间建立，在市场价格穿过![p](img/daecc39de4dc7417beb137da548b5756.png)之后。为了清晰起见，以下模型与唐尼和布肖所做的工作不同，且不够复杂，但我认为这是一种很好的捕捉直觉的方法。7

作为一个说明，考虑在结算价格从![p_0](img/033eafca0af13235ff135bf1448a2ab7.png)瞬间降至![p_1](img/b716c197fcad69246a31697549e730b7.png)后潜在订单簿发生了什么。起初，在![p_0](img/033eafca0af13235ff135bf1448a2ab7.png)和![p_1](img/b716c197fcad69246a31697549e730b7.png)之间的供给报价将为零：

![](https://mechanicalmarkets.wordpress.com/wp-content/uploads/2017/04/latentliq-initialpricedrop-svg.png)

之后，在这个新的间隙内，潜在的卖单将开始积累。我们假设 ![t(p)](img/8076ca7051d09aaf0d01853db0284752.png) 自价格跌破 ![p](img/daecc39de4dc7417beb137da548b5756.png) 起，![\rho_{S}](img/d8df4abe198dbd354542c839c026f52a.png) 仅作为时间的函数增长：![\rho_{S}(t(p))](img/d10fd1fba1cc3d9fab4654b68163594f.png)。[8] 函数![\rho_{S}(t)](img/f3b4be90aded6db04193a50450f73454.png) 的确切形式并不重要。

如果市场在这次初始价格下跌后没有变动，![t_1](img/b0bdd8d763854e204ea326da89b90c52.png) 时间后，潜在的订单簿将得到补充。在 ![p_0](img/033eafca0af13235ff135bf1448a2ab7.png) 和 ![p_1](img/b716c197fcad69246a31697549e730b7.png) 之间，将有数量 ![rho_{S}(t_1)](img/a96591625366c981c3ac959c40cbd3dc.png) 可供：

![](https://mechanicalmarkets.wordpress.com/wp-content/uploads/2017/04/latentliq-pricedrop-t1later-svg.png)

要计算 ![t(y)](img/d7cefb908140104e107f64adbd46389c.png) 的期望值，我们需要自价格距离现价 ![y](img/4d2c4d231bb45c490a6d88946970f81f.png) 的时间的概率密度：![\mathbf{p}_{y}^{LPT}[t]](img/261de928980b8329c9e6a5f496391ddb.png)。对于一个时间可逆的过程，这个分布与第一次通过时间的分布相同：![\mathbf{p}_{y}^{FPT}[t]](img/8a2e1c750a61d4c6db3d27d3c63ad6e0.png)。

对于连续时间布朗运动，第一次通过时间分布是众所周知的：

![y](img/4d2c4d231bb45c490a6d88946970f81f.png):

当 ![y \ll \sigma \sqrt{t}](img/fac970cb40b09653cc6a9604f29d97e9.png) 时，这是线性的 ![y](img/4d2c4d231bb45c490a6d88946970f81f.png)：

![y](img/4d2c4d231bb45c490a6d88946970f81f.png) 的边际供应约为：![\mathbf{p}_{y}^{FPT}[t] \approx \frac{y}{\sqrt{2\pi \sigma² t³}}](img/d4da148bc88a9447b2de89c72dd9ada8.png)

平均边际供应曲线是线性的，![y](img/4d2c4d231bb45c490a6d88946970f81f.png)是：

![y](img/4d2c4d231bb45c490a6d88946970f81f.png) 的期望是：![\mathbf{E}_{t}[\rho_{S}(t)] = \int_{0}^{T} \rho_{S}(t) \mathbf{p}_{y}^{FPT}[t] dt \propto y](img/51ce4c322c3930c2d4cd70c8023fb147.png)

其中 ![T](img/466f335a8268c61b30c4bbc675095312.png) 是市场运行的总时间。

因此，预期累积供应是 ![y](img/4d2c4d231bb45c490a6d88946970f81f.png) 的二次方：![\mathbf{E}_{t}[S(y)] = \int_{0}^{y} \mathbf{E}_{t}[\rho_{S}(y')] dy' \propto y²](img/63839148f2315f51fef48c14e80ba7c5.png)。

模型在足够大的![t](img/f1c9888691539079d4bb777ad80249bb.png)时应该会失败，因为从上次价格达到当前水平以来已经过去很长时间了。例如，如果油价超过了一年的最高点，达到了每桶 60 美元，那么我们可以预期边际供应接近 60 美元的水平会反映出石油开采的真实世界经济学。所以很明显，模型在![t=1yr](img/b3ecce6eb98bc70500a679d3ab0a0320.png)的石油市场中不应该起作用。但是，如果油价仅仅超过了当天的最高点，边际供应可能只是一个与那段时长有关的机械函数。我们可以认为，当![t](img/f1c9888691539079d4bb777ad80249bb.png)足够长，使得企业能够对新高的价格或低的进行反应时，模型将开始失效，这应该与商业决策之间的典型时间(![t_{InterDecision}](img/8f9d3c7b5673820763962f2a2dee09e5.png))相当。在这种情况下![W_{saddle} \sim \sigma \sqrt{t_{InterDecision}}](img/76a66a7c8cb537dde8c3f27b3dc1bb0a.png)，对于流动性较差的市场来说可能会相当大。

# 离散化过程

如果![\tau > 0](img/8744154aea2b2d449138379c90ee9a87.png)，在批量拍卖中，市场在每个批次周期![\tau](img/cd658e7d265e9e2b16272c4001abe15f.png)内都会清除，价格过程变得成为离散时间随机游走。无限长的![\tau](img/cd658e7d265e9e2b16272c4001abe15f.png)应该会在本文顶部恢复未清的、经典的供需曲线。所以，随着![\tau](img/cd658e7d265e9e2b16272c4001abe15f.png)的增加，我们预计会从布朗运动二次供应过渡到线性 regime。

为了得到离散市场的平均供应曲线，我们需要首次 passage 时间分布。当随机游走的

![\mathbf{p}_{y}^{FPT}[n] \approx (\frac{1}{2 \sqrt{\pi n³}} + \frac{y}{\sqrt{2\pi \sigma_{step}^{2} n³}}) e^{-y² / (2 \sigma_{step}² n)}](img/6cd9b4061377004bfc1a4c933bb0fbde.png)

其中![n](img/872ad603d260a26b8b46fc27a9e98c9d.png)是随机游走所采取的步骤数，![\sigma_{step}²](img/72f976b21f719e2228a60e43da249616.png)是每个步骤的价格变动的方差。当![n \to \inf](img/b300deed47bdf6d8aa934d98eb894626.png)并且![\frac{y}{\sqrt{n}}](img/45c40fa45027d260186407374e4ad26b.png)有限时，这个近似是有效的。步数与连续时间有关，通过![n = \frac{t}{\tau}](img/b64326a72cf12e5404422b3aced3dd26.png)。如果基础过程是布朗的，那么![\sigma_{step} = \sqrt{\tau}\sigma](img/22dbfc6e119e8748c014ec9c7e1be073.png)。

当价格过程具有典型步长 (![y](img/4d2c4d231bb45c490a6d88946970f81f.png)) 微小于距离市场价格 (![y](img/4d2c4d231bb45c490a6d88946970f81f.png)) 的距离的步长 (![y](img/4d2c4d231bb45c490a6d88946970f81f.png))（![\sigma_{step}](img/9c1d742fbb0554d80927f4649c898870.png)），那么第二项将占主导地位，此时 ![E_{t}[\rho_{S}(t)]](img/485414731accd4556c0ddd7bd914c524.png) 与连续布朗运动情况相同。也就是说，当 ![t \ll \frac{y²}{\sigma²}](img/a9da4ed55a22e8558f2a9812ef6ebac9.png) 时，累积供应与价格呈二次变化。

当过程被大量离散化时，![y](img/4d2c4d231bb45c490a6d88946970f81f.png) 微小于 ![y](img/4d2c4d231bb45c490a6d88946970f81f.png) 并且第一项占主导地位时，这将近似为常数。因此，边际供应将是常数，累积供应将与 ![y](img/4d2c4d231bb45c490a6d88946970f81f.png) 成线性关系。

这个结果与 Donier 和 Bouchaud 的相同。实际上，如果我们在 ![\mathbf{p}_{y}^{FPT}[n]](img/968bf6f9ee78d0a8e70b4d7ced67883a.png) 中对 ![\frac{y}{\sigma_{step}\sqrt{n}}](img/dfef04461568528262d7bf3faa7f98f4.png)（接近市场价格）展开到一阶，那么我们得到：

![E_{n}[\rho_{S}(n)] \approx L(y + u_0 \sigma \sqrt{\tau})](img/0bc43329f433839bc0908ec5461a4292.png)

其中 ![L](img/aebd3c20fb323c2f55eac7c952322a6a.png) 是通过积分 ![t](img/f1c9888691539079d4bb777ad80249bb.png) 获得的某个常数，由 Donier 和 Bouchaud 鉴定为流动性度量。而 ![u_0=\sqrt{\frac{1}{2}} \approx 0.71](img/88feecb53ed726b0ca900a7df4bce83e.png) 是一个常数，与 Donier 和 Bouchaud 获得的常数 ![u_0 \approx 0.82](img/5d60983414cd6d991f420832cddaaf7a.png) 相差不远。[11][12]

因此，缓慢清算的市场——其强烈离散化——可能没有鞍区。[13]

# 当价格过程是 Lévy 飞行时的供给/需求曲线

上述渐近性适用于一类具有有限方差的随机游动，但市场可能具有更厚的尾部价格波动，特别是在较短时间尺度上。如果 Lévy 飞行的指数为 ![0 < \alpha < 2](img/a983c573e6853cdd3a62898010c4fec7.png)，则具有发散方差和幂律尾部的价格增量 (![x_{t} = p_{t} - p_{t-\Delta t}](img/9b2ada0b83ed4f3e3663173e314a85df.png))：![\mathbf{p}[x] \sim \frac{1}{|x|^{\alpha + 1}}](img/8087ff15e28058fecc89c6bbbaf539d0.png)。

Lévy 飞行的首次穿越时间具有渐近概率密度函数：[14]

![p_{y}^{FPT}[t] \sim \frac{y^{\alpha / 2}}{t^{3/2}} ](img/9c172ddb63af1bc0a192fb24a3ee71ba.png) 当 ![t](img/f1c9888691539079d4bb777ad80249bb.png) 较长时。[15]

这种分布平均给出累积供应曲线![S(y) \sim y^{(2+ \alpha) / 2}](img/2b7066f49eb91eb8d8155ddc8ff90c8e.png)。并且市场订单将具有价格影响![\mathcal{I}(q)=S^{-1}(q) \sim q^{2 / (2+\alpha)}](img/fe6e3d932888a3b3194d9a021dab9197.png)。作为一个例子，![\alpha=1.5](img/1a2f860482442c4a75032d252ed42af0.png)将对应于一个相当“跳跃性”的市场，并且将具有![S(y) \sim y^{1.75}](img/3b68b6f3727ca8b60fd6a5973f6da5c2.png)和![\mathcal{I}(q) \sim q^{0.57}](img/4b26e3810cc35279af1b5085d8691067.png)。 [16]

# 子扩散价格过程的供需曲线

一个子扩散的波动性随时间尺度的增加比普通布朗运动的波动性增加得慢。例如：![\sigma_{\Delta t}² \sim \Delta t^{\gamma} ](img/210ee2a25d7a02d73cf3868c03689117.png)。当![\gamma = 1](img/80313789978bfeab0eff804dc99ea760.png)时，波动性随时间尺度的增加以通常方式对布朗运动进行：与时间尺度成线性。当![0 < \gamma < 1](img/27db510be2ce2814b178c83c2d65e27f.png)时，该过程是一个子扩散。子扩散市场在某种意义上具有均值回归，即价格波动未来可能被逆转。因为子扩散市场具有“记忆”，所以它们被认为是“无效”的。 [17]

子扩散的第一个 passage 时间分布是渐进的：[18]

![\mathbf{p}_{y}^{FPT}[t] \sim \frac{y}{t^{1 + \gamma / 2}} ](img/39c7c475de6b4b72d0a0a8924be8fc64.png)

这与普通布朗运动的线性价格依赖性相同。因此，累积供应量再次是二次的，市场影响再次是平方根。

某些类型的“效率”可以[导致平方根价格影响](https://mechanicalmarkets.wordpress.com/2016/08/15/price-impact-in-efficient-markets/)。但如果这个模型大致准确，那么像子扩散这样的“无效”市场也可能有平方根影响。

**更新**：Benzaquen 和 Bouchaud 刚刚研究了子扩散的[反应-扩散模型](https://arxiv.org/abs/1704.02638)。他们表明潜在的订单簿是局部线性的（等式 10），这与这里粗略的第一 passage 分析相似。对于快速执行的元订单，他们得到![\mathcal{I}(q) \sim \sqrt{q}](img/ee7ed672024362879bfc11aff8f62223.png)。但对于在执行中途给潜在订单更多反应时间的慢速元订单，他们得到![\mathcal{I}(q) \sim q^{1-\gamma / 2}](img/8a2624bd6ed62e6eb4ee4746c29a0b54.png)。

# 扩散和子扩散中影响的数量级缩放

我觉得这个结果有趣，因为它乍一看似乎与最简单、数量级的“推导”平方根影响法则相矛盾。但仔细观察后，我认为数量级逻辑与子扩散和普通扩散具有类似的影响缩放是一致的。

如果市场是布朗运动，则其价格变化将与 ![\sigma \sqrt{\Delta t}](img/8d723c5f7449bbaa245936b5fab0e1f3.png) 成比例。价格发现的观点之一是，价格变化的一小部分（数量级为 1）来自交易者的影响。因此，元订单的影响将与订单持续时间平方根大致成比例： ![\mathcal{I} \sim \sigma \sqrt{t_{OrderDuration}}](img/1ba923f598fa26c2510f30d8e88320df.png)。市场总体成交量随时间以恒定速率累积 (![V](img/ed31064250f2c63fd3e7e1c9be00bf8e.png))，所以规模为 ![q](img/d5dff62051727d5390f29a8eb12a4588.png) 的元订单会持续 ![t_{OrderDuration} \sim \frac{q}{V}](img/662b405f5bd96f164ca173e68b880fd0.png) 时间。这给出了 ![\mathcal{I}(q) \sim \sigma \sqrt{\frac{q}{V}}](img/233b9d19d455e54476d1a62b08b5f31a.png)。

现在，如果市场是亚扩散的，则其价格变化随时间更慢： ![\Delta p \sim \Delta t^{\gamma / 2} ](img/9446d8984fc3c0fc26cfd30a4576326f.png)。如果上述论点其他一切均相同，那么我们会得到 ![\mathcal{I}(q) \sim q^{\gamma / 2} ](img/17e8eaefe995c683efebb1b5d02cfdd8.png)。但没有理由期望亚扩散市场的成交量应以恒定速率发生于时钟时间。

亚扩散可以被重新表述为具有独立增量的过程，其中步骤之间的变量时间具有长尾。在这种表述下，步骤可能对应于交易活动——每个步骤的成交量大致为 ![V_{step}](img/ee1a320b0337a7d53aaa7d6ba54d31e4.png)。元订单会持续 ![N](img/56100eb36e864722bbd3a37237be8672.png) 个步骤，其中 ![N \sim \frac{q}{V_{step}}](img/7ce40cffa192010b024e5a2bae39d443.png)。这种亚扩散的步骤长度具有有限方差 ![\sigma_{step}²](img/72f976b21f719e2228a60e43da249616.png)，因此我们可以遵循与布朗运动案例相同的论点，用步骤计数代替时间： ![\mathcal{I}(q) \sim \sigma_{step}\sqrt{N} \sim \sigma_{step}\sqrt{\frac{q}{V_{step}}}](img/6092eb8ffacc0cc50c2dde0285211498.png)——这与平方根比例相同。

# 结论

市场行为即是群体行为，而且一个群体可能比其中的个体更容易预测。唐纳器和布绍 aud 在其松散的解释中表明，当市场是机械且乏味的时候，它们将具有大致上二次累积供需曲线。现在，很多人认为市场并不乏味！即使许多市场确实在鞍点运行，鞍区可能并不宽泛。但是如果有的话，小价格变动对生产和消费的影响可能几乎为零，而大幅价格变动可能产生巨大影响。这与标准直觉不同。

1 这个图显然是启发性的。供需曲线众所周知有很多形状，可能是[非单调的](http://www.nber.org/papers/w13243)，并且在局部最大化交易量可能有一个以上的价格。

2 在![p*](img/fc13cdcdcef4fb20d1b4cedc27f9111b.png)附近的供需曲线应该（可能）关于![p*](img/fc13cdcdcef4fb20d1b4cedc27f9111b.png)是对称的，如果我们对给定市场的一些情况集合进行平均。

3 借鉴他们与 Bonart，Deremble，de Lataillade，Lempérière，Kockelkoren，Mastromatteo 和 Tóth 的早期工作（例如[2014](https://arxiv.org/abs/1412.0141)和[2011](https://arxiv.org/abs/1105.1694))。

4 即使大的价格变动几乎不影响供需，它们仍然可以发挥重要的经济功能。交易者的观点和信息被融入价格中，当市场透明时，这些价格提供了长期商业决策的有用信号。

5 [Waelbroeck 和 Gomes](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2291720)的第 1 表和第 13 图表明，大部分机构股票的元订单期限少于几天。

6 需求方面也是类似的。为了简化，我们只讨论供给侧。

7 潜在流动性通常是不可观测的，因此我们无法轻易地测试假设：潜在流动性在给定价格随着时间的推移而建立。但是，潜在流动性可以通过订单簿来衡量——如果一个市场被高度金融化、透明，并且由不隐藏其意图的交易者主导。可以说，比特币就是（或曾经是）这样的市场。

8 我们可以在![\rho_{S}](img/d8df4abe198dbd354542c839c026f52a.png)中添加一个独立的随机噪声项，这不会影响结果。假设![\rho_{S}](img/d8df4abe198dbd354542c839c026f52a.png)没有显式的价格依赖性，这与 Donier 和 Bouchaud 的例子（常数![\omega](img/46911229ccd094f60644798290dc3e43.png)和![\nu](img/79629a3448ec665de2bbf3f2c0caca1c.png)）相似。这个假设显然是错误的，但如果足够接近市场价格，它可能是合理的。

参见企业的反应时间可能比人类决策的时间尺度长得多。特别是在所讨论的市场不透明或尚未成熟的情况下。例如，如果一个农民从种植橄榄转向种植杏仁，她的果园可能需要几年时间才能再次产生效益。因此，杏仁的价格可能需要达到多年的高点，这样她才会足够自信地切换作物。但是，如果农民能够对未来的产量进行套期保值，她在经济上合理时可能会迅速决定切换作物。或许一个发达的期货市场将这个模型的有效范围从![t \lesssim 1yr](img/f085bfdaab17a05d3ce1d796c131203a.png)减少到了![t \lesssim 1day](img/cf40ca8964b05990a0183bd9d73c018a.png)。

参见在[Majumdar](https://arxiv.org/abs/0912.2586)的文献中第 38 个等式及其引用中的详细信息。我将等式 38 的累积分布函数(CDF)转换成了概率密度函数(PDF)，并去除了一个非主导项。

参见[等式 22](https://arxiv.org/abs/1506.03758)。

参见 Sparre-Andersen 比例适用于任何具有价格变动连续和对称分布的马尔可夫过程：对于很大的![t](img/f1c9888691539079d4bb777ad80249bb.png)，首次穿越时间分布必须像![t^{-3 / 2}](img/e61e184d019ae64b91176fb54abbe24a.png)那样衰减。因此，为了使![t](img/f1c9888691539079d4bb777ad80249bb.png)的期望值收敛，我们必须有![\rho_{S}(t) < \sqrt{t}](img/9cc74f13b81ff5816c157f0a4fbaff5f.png)对于很大的![t](img/f1c9888691539079d4bb777ad80249bb.png)（假设![\rho_{S}(t)](img/f3b4be90aded6db04193a50450f73454.png)是单调递增的）。也就是说，在给定价格下的边际供应必须比自市场处于该价格以来时间的平方根增长得更慢。潜在流动性与首次穿越时间之间的联系在非常长的![t](img/f1c9888691539079d4bb777ad80249bb.png)时不会保持，但是这可能提供了潜在流动性能够恢复的速度的一个宽松界限。

参见根据该模型，当价格变动足够大（因此最后一次穿越时间长）时，缓慢清除的供需曲线仍然由二次项主导。但是，在非常长的时间尺度上，当企业能够对价格变动做出反应时，模型应该会失败。尽管如此，如[9]所述，如果市场缓慢且不透明，模型的有效时间尺度可能会更长。

参见例如，在[Koren 等人](https://arxiv.org/abs/0706.3641)的文献中第 10 个等式。

参见[图 2](https://arxiv.org/pdf/0706.3641.pdf)显示，经过几个时间步之后，这种渐进结果的收敛速度相当快。

也许 impact 比布朗运动的情况更陡峭并不令人惊讶。直观地说，Lévy 尾巴使得市场更加“动量驱动”。在 Lévy 类型的市场中，一个发起价格运动的交易者可能会发现市场很快远离她。这里使用的 Lévy 过程具有独立增量，但我们可以在连续时间内的“中增量”想象独立性 breakdown。即，动量交易者可能在时间步长中间交易是可想象的。

顺带一提，Koren 等人 [17] 显示 Lévy 飞行中的平均跳跃长度发散。跳跃长度可以被理解为止损订单的利润，*如果*它们在价格跳跃中间执行并且能够在尾事件期间击中流动性。这些都是很大的“如果”，但潜在的无限利润可能部分解释了止损订单和短期动量策略的流行。这也可能解释为什么交易员不愿意将太多流动性远低于当前价格。

在低交易成本的亚扩散市场中，押注均值回归是一种盈利的策略。如果你知道有类似这样的电子市场，请让我知道。

即使亚扩散在电子市场中很少见，不同资产的线性组合仍然可能是亚扩散的。典型的“配对交易”涉及两种资产价格之间的均值回归差。另外，亚扩散在更广泛的场外经济中可能比我们预期的更常见。

[见 Metzler 和 Klafter 文章](http://www.agnld.uni-potsdam.de/~metz/papers/2000_MeKla_PhysA278.pdf)中第 30 式序列展开的第一个非常数项。式 30 是生存概率（即首次穿越时间累积分布函数），其概率密度函数是时间导数。当![y \ll \sqrt{ K_{\gamma}t^{\gamma} }](img/5c9684c98cf5c3091a322efdf2990d1b.png)时这个近似是有效的。![K_{\gamma}](img/e9095817405a94dd5122c4df0feaa0a8.png)是“分数扩散系数”，与![\sigma²](img/396a8a13bcae7e4896e43b01c3ddae7d.png)（当![\gamma=1](img/7a86eda449c95d57b0d2975d7a7877f1.png)时的情况)相对应。

请注意，亚扩散不是马尔可夫过程，所以 Sparre-Andersen 规模 [12] 不适用。流动性必须比![\rho_{S}(t) < t^{\gamma / 2}](img/e1b6e9b2229353c425f01984d6b1e144.png)更慢地补充，对于大的![t](img/f1c9888691539079d4bb777ad80249bb.png)。

相关等待时间也可能导致亚扩散 [19] 在具有独立增量的过程中。

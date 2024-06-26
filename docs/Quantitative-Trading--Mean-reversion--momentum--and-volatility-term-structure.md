<!--yml

分类：未分类

日期：2024-05-12 18:56:30

-->

# 量化交易：均值回归、动量和波动性术语结构

> 来源：[`epchan.blogspot.com/2016/04/mean-reversion-momentum-and-volatility.html#0001-01-01`](http://epchan.blogspot.com/2016/04/mean-reversion-momentum-and-volatility.html#0001-01-01)

众所周知，波动性取决于测量频率：5 分钟回报的标准差与日回报的标准差不同。精确地说，如果 z 是日志价格，那么间隔τ采样的波动性为 volatility(τ)=√(Var(z(t)-z(t-τ)))，其中 Var 表示在许多样本时间上取方差。如果价格真的遵循几何随机游走，那么 Var(τ)≡Var((z(t)-z(t-τ)) ∝ τ，波动性仅仅是采样间隔的平方根。这就是为什么如果我们测量日回报，需要将日波动性乘以√252 以获得年化波动性的原因。交易员也知道价格并不真的遵循几何随机游走。如果价格是均值回归的，我们会发现它们并没有像随机游走那样迅速离开其初始值。如果价格是趋势性的，它们*更快*地偏离。总的来说，我们可以写成 H 被称为“Hurst 指数”，对于真正的几何随机游走等于 0.5，但对于均值回归的价格小于 0.5，对于趋势性价格大于 0.5。如果我们对一个均值回归的价格序列的年化波动性进行年化，即使两者在 5 分钟柱上测量的波动性完全相同，它最终的年化波动性也会低于几何随机游走。对于趋势性价格序列则正好相反。例如，如果我们对 AUDCAD 这个明显均值回归的时间序列进行测试，我们会得到 H=0.43。所有上述内容许多交易员都知道，实际上在我的[书](http://www.amazon.com/Algorithmic-Trading-Winning-Strategies-Rationale-ebook/dp/B00CY5HC0U/ref=as_sl_pc_qf_sp_asin_til?tag=quantitativet-20&linkCode=w00&linkId=OKVO7DYTPENVN5Y7&creativeASIN=B00CY5HC0U)中有讨论。但更有趣的是，Hurst 指数本身在某些时间尺度上可以发生变化，这种变化有时意味着从均值回归到动量市场的转变，反之亦然。为了看到这一点，让我们将波动性（或更方便的是，方差）作为τ的函数绘图。这通常被称为（实际）波动性的期限结构。从熟悉的 SPY 开始，我们可以使用从 1 分钟到 2¹⁰ 分钟（~17 小时）的中点价格计算日内回报，并将 log(Var(τ))对 log(τ)绘图。下面显示的拟合非常好。（点击图表以放大）。斜率除以 2 就是 Hurst 指数，结果为 0.494±0.003，这非常轻微地倾向于均值回归。

但如果我们为 SPY 的日回报执行相同的操作，对于 1 天到 2⁸（=256）天的间隔，我们发现 H 现在是 0.469±0.007，这*显著*地倾向于均值回归。

    我们可以看到，在大约 16-32 天的时间范围内，波动率与从日内频率外推的直线分离。那里我们应该从动量策略转向均值回归策略。

一个有趣的侧注：当我们计算跨越两个交易日的回报期间的方差并将它们作为对数(τ)的函数绘图时，τ应该包括市场关闭时的小时数吗？结果证明答案是是的，但并不完全。为了产生上面提到的图表，其中日方差最初与日内方差落在同一直线上，我们必须将 1 个交易日视为相当于 10 个交易小时。不是 6.5（对于美国股票/ETF 市场），也不是 24。当然，不同工具的等效交易小时数是不同的。

结论：SPY 上的均值回归策略在日内交易应该比日内交易更有效。我们可以对 USO（WTI 原油期货 ETF）做同样的分析。日内 H 值为 0.515±0.001，表明有明显的趋势行为。日 H 值为 0.56±0.02，甚至更有明显的趋势。所以，在任何合理的 时间尺度上，动量策略都应对原油期货有效。现在让我们转向 GLD，黄金 ETF。日内 H=0.505±0.002，略有趋势。但日 H=0.469±0.007：明显均值回归！动量策略在黄金日内可能有效，但均值回归策略在多日肯定更有效。转变发生在哪里？我们可以仔细检查期限结构：

均值回归策略不仅仅是配对交易。找出如何在当前有利于这类策略的低波动率环境中蓬勃发展。

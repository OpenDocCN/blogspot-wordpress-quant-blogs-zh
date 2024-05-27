<!--yml

分类：未分类

date: 2024-05-18 13:55:50

-->

# 三大骑士 | Quantivity

> 来源：[`quantivity.wordpress.com/2009/07/25/bias-stationarity-ergodicity/#0001-01-01`](https://quantivity.wordpress.com/2009/07/25/bias-stationarity-ergodicity/#0001-01-01)

传统观念告诉我们量化交易很难。然而，很少有人知道它具体为什么难。此外，不同类型的量化交易遭受的复杂性也不同，例如：数学建模、信息获取（例如：逐笔数据）、计算设施、执行设施（例如：低延迟）、风险管理（例如：实时 VaR）以及杠杆（例如：RegT 对 [组合保证金](http://www.sec.gov/rules/sro/nyse/2006/34-54918.pdf)）。

在所有复杂性中，许多都是由量化交易的三大骑士引起的：*偏差*, *平稳性*, 和 * ergodic 性*。

人类心理学告诉我们人类特别容易受到[归属偏差](http://en.wikipedia.org/wiki/Attributional_bias)的影响：

> 影响我们确定事件或行为责任归属方式的心理偏差。

CNBC 简直是在做归属偏差的生意：一些自以为是的评论员试图解释市场为什么会有那样的表现，尽管所有人都深知这样的解释最多是不完整的（至少也是完全错误的）。这种偏差促使人们提出这样的假设：计算机系统编程交易比人类做得更好。

这种困难进一步加剧了一个基本错误的假设：关于金融市场的随机性（黑天鹅事件除外）。具体来说，绝大多数统计分析技术都基于以下假设（这通常是未声明的）：

> 一个随机过程不会随时间改变其统计特性，这样的特性（比如过程的理论均值和方差）可以从该过程的一个足够长的样本（实现）中推断出来。([维基百科](http://en.wikipedia.org/wiki/Stationary_ergodic_process))

这种谬误源自[概率论](http://en.wikipedia.org/wiki/Probability_theory)，其正式含义是指随机性可以被建模为一个*平稳 ergodic 过程*。平稳性指的是统计特性不随时间改变。 ergodic 性指的是这样的特性可以从随机过程的一个足够长的样本中推断出来。不幸的是，对于大部分定量金融来说，这两个概念都是不正确的（否则，每个一年级计量经济学研究生都会很富有）。

这种谬误在金融领域比比皆是，不仅在定量世界里：

+   过去的表现：许多人根据过去的表现来做投资决策（俗称“追涨”），希望未来会像过去一样。

+   可信度：许多人将可信度赋予那些过去预测成功的人，这受到了我们[名人文化](http://www.amazon.com/Life-Movie-Entertainment-Conquered-Reality/dp/0375706534)的加强。

+   资产配置：许多人根据自己的投资组合采用源自[现代投资组合理论](http://en.wikipedia.org/wiki/Modern_portfolio_theory)的简化技术，从经典的 60/40 到新的“捐赠”模型不等。

+   期权定价：从[布莱克-斯科尔斯](http://en.wikipedia.org/wiki/Black%E2%80%93Scholes)开始，大部分数学金融都是基于假设平稳 ergodic 性的数学形式主义（例如，随机游走，布朗运动等）。

而且，可以说最糟糕的是，甚至连最严谨的统计学家也会被其吸引：时间序列分析（从[回归分析](http://en.wikipedia.org/wiki/Regression_analysis)到[主成分分析](http://en.wikipedia.org/wiki/Principal_component_analysis)），其数据跨越几十年。这种思维方式通常通过引用[大数定律](http://en.wikipedia.org/wiki/Law_of_large_numbers)来证明：“数据越多越好”。不幸的是，缺乏稳定性比缺乏大数据对统计学的破坏性更大。

这三个因素经常结合在一起，使量化交易变得复杂：假设平稳 ergodic 性的统计技术用于构建系统，其作者将这些技术的解释能力归因于一组工具的行为。不幸的是，在实践中，*产生的统计模型往往不够稳定，因此在产生一致利润方面有限的成功*。

鉴于这三位先驱，挑战在于以最小化这些误区的方式进行交易。

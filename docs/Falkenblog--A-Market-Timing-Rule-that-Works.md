<!--yml

类别：未分类

日期：2024-05-12 20:35:25

-->

# Falkenblog：一个有效的市场定时规则

> 来源：[`falkenblog.blogspot.com/2012/02/market-timing-rule-that-works.html#0001-01-01`](http://falkenblog.blogspot.com/2012/02/market-timing-rule-that-works.html#0001-01-01)

金融最有趣的事情之一是，虽然过去似乎是可以预测的，但在实践中，使用简单规则很难超过被动指数。

[Ivo Welch 和 Amit Goyal](http://research.ivo-welch.info/journalcopy/2008-rfs.pdf)

显示了一堆信号，比如股息收益比，在事后可能有效，但实时情况下无法提高股票收益率在业务周期中的表现。这种偏见最好的直觉是，如果我们取一个由简单时间序列生成的数据集，并绘制该股票的股价与未来收益的关系图，我们的样本中股价与未来收益之间会有很强的负相关性，尽管我们实时知道仅仅股票价格并不能预测股票收益。这种悖论的结果是为什么许多人确信市场是非理性的，或至少容易通过 if-then 逻辑进行无数改进的原因，因为他们从未尝试过他们确信存在的规则（以及为什么 E-Trade 和 Ameritrade 将市场营销视为提供给业余者关于趋势和比率的大量信息可以相对简单地带来更好的回报--与仅仅更多的佣金相反）。

尽管如此，许多人提出了这样的建议，随着年龄增长，应该将更多的财富比例地配置到现金中，一个基本规则是你的年龄以百分比的形式应该是你的债券配置（例如，29 岁的人是 29%）。虽然这种建议很常见，但大多数学者认为这样的建议是误导性的，因为

[Robert C. Merton 和 Paul A. Samuelson](http://zonecours.hec.ca/documents/H2006-1-640175.Texte6-30-253-00-E05-Live-cycleFinance...(2).pdf)

多年来，我写了很多文章，论证这些是基于对长期数据的误解，而这些数据恰好在过去 120 年里在美国运行良好。

我没有讨论那个论点，即一个人应该根据自己的投资视野或人力资本水平不同而进行不同的分配，相反，我着重于从波动性的可预测性中得出的含义。考虑下面方差预测中隐含的简单 10 天移动平均数。

EMAvar(t+1)=(1-λ)*ret(t)²+λ*EMAvar(t)

当λ=0.9 时，这是一个大约 10 天的指数衰减移动平均数。现在，使用来自肯·弗伦奇的市场回报数据的每日观察，

[网站](http://mba.tuck.dartmouth.edu/pages/faculty/ken.french/data_library.html)

（它自 1963 年以来的每日回报），我们得到了非常显著的可预测性。这个事实是建模

[GARCH](http://en.wikipedia.org/wiki/Autoregressive_conditional_heteroskedasticity)

金融时间序列的建模，以及为什么罗伯特·恩格尔因此获得了诺贝尔奖。波动性是极具可预测性的：

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEieZhgDCzIEEnAzLXMG95pphq16fdVj389tAlNZ6MvbKrcQ4RuU4qZFyYbNzvsXOywfthnhPuut0K7D2qMUgUwFtyzpwGf79z6Ka5Cl4-ZOeWuzJetDjMjAAeoTVq44su3Rp4fc3Q/s1600/fcstvsact.png)

相比之下，收益与波动性预测的相关性不高（这里的数据根据方差预测分为 20 组）：

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjxXOtDBBF59M5BJ1lN5lDi-tILwj9paBfWM89FkDmVTOkPIRxSUVtBYKJyzVwrGNySrqligKoTQl2XyO5Zq6vwjrsZCq4CEmvTY3719FgFomGVfbMT0Du-eTixLGXg-kcuDB7niw/s1600/volfcstret.png)

波动率预测与算术收益率存在弱相关性，而与几何收益率则极弱相关。简单的推论是，通过避免那些没有相应回报溢价的高波动时期，您可能能够提高夏普比率。正如 Welch 和 Goyal 所强调的，关键在于这是否是一种在实时消失的模式，在上述图表中，“高”和“低”只有在看到发生了什么之后才能确定；一个有用的规则查看“点时间”数据，这不是前瞻性的，而这是大多数规则失败的地方。

请考虑以下规则：

+   如果 Ema(Variance) < [1.5*2 年 Ema(方差)滚动平均值]，则将 100% 投资于股票。

+   否则，将 100% 投资于国库券。

+   只有在过去一个月内未更改配置时才更改配置。

请注意，该标准仅仅是向后看的，只是指出如果方差估计值太高。最后一点只是防止对大型投资组合进行一些不切实际的快速更改，并且实际上并没有对结果产生太大影响。这产生了以下结果：

数据来自 1965 年至 2011 年。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjYT-V9aeMDgR2oIIFgHXYHbXJ20T-5ngtFEPs4AoOen_JEqKgmzRlpoMAYRyxTPa7BrGGnGkPZeEQANXLo5-Jb8wn6adSfqDMhInszU8_FoV9mUOCgZ5bBhkcZLs6P47iUqhv8BA/s1600/rettable.png)

因此，定时规则显著增加了夏普比率，从 0.25 提高到 0.43。移除了 33% 的波动性，可以与“最小方差组合”相媲美。也就是说，这些方法还可以将您的波动性相对于被动策略降低 30-40%，而不会牺牲总收益（通常会增加几个百分点）。最大回撤从 55% 降至 47%，这并不多，但是定时策略在 2009 年错过了一次相当大的损失，因此更重要的是这些 50% 左右回撤的频率从 2 降至 1。

这个策略在整个时间段内产生了平均 68% 的“多头”头寸，因此我将其与静态 68%/32% 的股票/债券组合进行了比较。在这里，可以看到这几乎没有改变夏普比率，尽管它大大降低了投资组合的波动性。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgRe18QHr5VC0p0z3nijKTvwdAdh7V2tYbzGsXlSYkAKpFToV9Y18-TOiM5hTa-QZHnHo8mmYmQ4-5tYnVGH_RXMj7qdSdjGkdPALXeRN6GIq4QO9MtGC5XULm65OfLCLV5j3Hvig/s1600/totret.png)

波动率定时可将您的投资组合波动率减少三分之一，而不会牺牲总回报，不像静态混合投资组合那样，其中多余回报是等比减少的。

有些人可能会说：“这很棒，但如果每个人都这样做会怎样？”嗯，如果每个人都定价于条件市场波动性（在 1960 年代被称为‘风险’），那么就会有一个动态风险溢价，正如标准理论所假设的那样。也就是说，从理论上讲，

资产需求=k*E(ret)/方差

这里的 k 是某个常数，并且这是一个标准结果（见

[这里](http://www.people.hbs.edu/rmerton/onestimatingtheexpectedreturn.pdf)

). 资产需求应与预期回报方差成反比，除非预期回报同时变动。预期回报与方差不同时变动，但在此之前，您最好遵循

[规范性的](http://en.wikipedia.org/wiki/Normative)

的含义

[现代投资组合理论](http://en.wikipedia.org/wiki/Modern_portfolio_theory)

，这可能不解释世界是如何运作的，但确实产生了一些有用的工具来处理您的投资组合。

结论是这样的：清理掉投资组合中最波动性的组成部分，跨时间和资产，您将略微增加您的回报并显著降低您的波动性。它之所以有效，正是因为它并没有提供给您一些如此吸引人的东西，以至于即使每个人都相信它有效，大多数人也不会使用它。在夏普空间中，这比从主动式到被动式共同基金的转换（本身就是一个好主意）的改进要大得多。

上述的一个推论是，随着 VIX 达到 18，相比其两年平均值 23，现在是重新投资于股票的时机。

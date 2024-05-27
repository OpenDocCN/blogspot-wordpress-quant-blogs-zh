<!--yml

分类：未分类

日期：2024 年 5 月 12 日 21:39:52

-->

# 鹰之群博客：R2s 和 Sharpes

> 来源：[`falkenblog.blogspot.com/2010/01/r-2-s-and-sharpes_18.html#0001-01-01`](http://falkenblog.blogspot.com/2010/01/r-2-s-and-sharpes_18.html#0001-01-01)

在策略模拟中，绩效指标有时被呈现为 R

²

. 这些很难解释，因为显然，1%的 R

²

在一天内的 1%的策略比 R 更好

²

在一个月内的 1%。年化夏普比率是一个好的焦点，因为历史上，股权风险溢价作为基准是一个很好的焦点，因为它是常见的和可行的（约为 0.4，和 6%的股权溢价，15%的年化波动率一致（我写过

[一本书](http://www.efalken.com/video/index.html)

我认为这可能更接近 0.1，但那是少数看法）。任何超过 0.5 的都相当好，而 1.0 以上的都很好。年化夏普比率的定义如下：

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiVhUkA5UqjBFHY9W3i8yIqdG8ahwWZInNe4niYODHTtWcz8jGIWo-nW-o50WfUXKVoVfw4ErREMqEwc-uhk3PP4ZbhyphenhyphenqIoSkMh5QYfnk_YFndfZ6GR5F0DRHMs91hHQTrEE8tJkg/s1600-h/Eqn020.gif)

通过年化夏普比率，我们可以进行直接的比较。由于回报与时间线性相关，标准偏差随时间的平方根增加，因此我们需要有一个公共时间来进行夏普比率的比较。

就许多策略而言，一种是根据特定的战术规则和预期收益模型预测组合的利润。例如，如果认为市场上涨，有几种方法可以利用这一点：购买期货，期权，牛市看涨价差等。这增加了结果的自由度，因为通常某些标准可以产生不同的夏普比率。

我会假设一个实施线性头寸规则，即头寸与策略的预期收益成比例。因此，如果预计收益为 1%，那么当预期收益为 2%时，长头寸就是前者的一半；如果预期收益为-1%，则短头寸正好与预期收益为 1%时的相反。影响夏普比率的是信号之间的比例关系，而不是绝对大小，因为不管我投资量是平均的$1k 还是$1MM，它的夏普比率都是一样的。至于线性是否最优，直觉上它几乎是最优的，基本上是说如果有条件的方差是不变的，你将下注的筹码是预期收益的两倍。

因此，假设我们正在预测收益，这可以是一个投资组合，也可以是一支股票，都无关紧要。某件‘东西’有一个预期收益。这有一个可预测和不可预测的成分。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiSgEK0Av3WFW-a9JqrwhEzA9wgUBzQhgqZeB5DO1mpn6I8vuz0dWzMyEMnLfeDV7zs_aREcl4vkE8UUUEbeVk7e4vIyORVszpe49F6mdxIFJz8z_TrKaNqqu_YJVQZx5W_UgsNpg/s1600-h/Eqn022.gif)

这里

*f*

是策略回报的可预测部分，ε是随机部分。考虑到线性头寸规则，预期回报简单地就是

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj1v-aROIxdKWhjLkIkuvFKrRUulunpWsBMezJAn1IR9qDnII4N7_UaMHM6_U_2pMndzuhFmgxzkAserGiSAYqoM3py2KyyvmWKyPL-QxKo_CK3r97DAyLhSUiTOf07shNsEj1JVw/s1600-h/Eqn024.gif)

假设策略和预测中的无条件预期回报超过无风险利率都是零是很有用的。在它们不是这样的情况下，那将是不属于“超额”的可预测回报，是资本成本。因此，我们有

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhdxBVIPOglUP5REkiqvLPlMEEl07slsgJ5lsjFIbFreLkCPOlJz5beHUcfeftfswj2OWdHxd-Qh3d7BH8MUjigK_7BZKxe66vadQj0sSdYupsOLokGgBpUggYDEBl8s0H-77o2nA/s1600-h/Eqn026.gif)

现在，两个高斯随机变量的乘积的方差，应用于

*f*

和

*ret*

，是

*Var(f⋅ret)=σ²[f,ret]+2σ[f,ret]E(f)E(ret)+E(f)²σ²[ret]+E(ret)²σ²[f]+σ²[f]σ²[ret]*

这个证明相当乏味（见

[Bohrnstedt and Goldberger, 1969](http://www.jstor.org/pss/2286081)

），而且关键地依赖于高斯分布，以避免来自更高阶矩形的额外复杂性（这就是我们喜欢正态分布的原因！）。

考虑到预期回报都是零，我们有

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi_FOAXzLumahwTLEekP5m0ghUnbuGdBUdb6TQTLonujeVFGRc43jLACkef78JZXLXVk9LcErvGCcxriOopVWA_JNkUIErImIW8F1sVj-3bG8ajkw2GJh7ML679yJ4Key54rocDNw/s1600-h/Eqn028.gif)

因此，策略的夏普比就是

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEi30BfHmCuqUtyOB3omo8DIvqQDJzrpAVzx79ouG8aTW_v7geZKD11FvqURSdo0Y3X62rsAL9SCyd8Ouni7XP7LB7Xa9O9mkPxiyEZD3E_A0nO6B-4gH3syRldiYRv6oMrVmB4CMw/s1600-h/Eqn029.gif)

现在，给定σ

[x,y]

=ρ

[x,y]

σ

[x]

σ

[y]

我们有

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgR6-ribWrmDTSY6eR49qEEOlgWOeqMkzhGoWL3MztbxylB_nDVjuOsiX8bBEHNFxka7XIQmTi5VbeI1EBd6Xi4zJoBdlSmO0PqZV9i6taqvXnJ-bwF-2kF6IW9OkACKHSDBuIFEQ/s1600-h/Eqn031.gif)

好处在于，分子ρ

[x,y]

，只是一个 R 的平方根

²

！也就是说，无论你的

*f*

，R

²

回报的回归

*f*

，这是你计算夏普比所需的知识。

最后一步是年度化，将其转换为统一的单位。我们只需要应用这一调整。对于不一定是在固定增量的日历时间内执行的策略，我们假定 t=每年的连续交易次数。这会产生以下调整：你把夏普比乘以每年的预期交易次数的平方根。所以，在这个等式中，确保你将预期交易次数 t 带入其中。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgV_w-0xZB6fZ7muOjREaXaJTXArjCEqp7DZHds4rWQt7aAZBR30etK7sXn5_1WWt8JDTzxgdBTYtH54ex2TSMY5JLLvaSoGXE_wTm3dzj0afWZhRUeTCs3cmtAtOJeGIpruoDIXg/s1600-h/Eqn054.gif)

或

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhQsnoxlNETw4LMg2a2BBjsrL2tgieRMSNQ2S7NXBwRez8ICstbUzisEHaubozgb5t2tYiUHmF_Tp339_kQQKJff4Au5IWquHuM2JjZ0Wq6MrfBzh3V2GZNPKVuCvE9XXvWpJECAg/s1600-h/Eqn052.gif)

所以，有个 R

²

, 并且交易频率，我们可以生成合理的夏普。例如，在下图中，我们看到了 R

²

夏普 1.0 策略的 Sharpe 值根据每年进行的交易次数而变化（例如，一个月的水平每年进行 12 次交易）。

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhUarBh7xBcOqaxh0R3n9fyvem2V0wigOJ5SQRLG2j-VBIvp1FlgL9vn-dgRYWESvhxV9m9l7YL-Aa8ChZVOtIsVtvib3W5Ciq2Bz8EXU1D4Su7JhyphenhyphenMSUlAdf2wm0jvfG3oCJzygg/s1600-h/sharpe.jpg)

所以，R

²

预测年度数据时，并不像同样的 R 一样有价值

²

超过 1 周。在某些程度上，这是显而易见的，但我认为有一个具体的公式来进行比较是很好的。一个重要的限制是这里没有考虑交易成本。策略的频率越高，交易成本的重要性就越高。

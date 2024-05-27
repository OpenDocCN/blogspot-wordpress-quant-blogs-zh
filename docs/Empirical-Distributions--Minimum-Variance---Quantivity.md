<!--yml

类别：未分类

日期：2024 年 05 月 18 日 13:51:49

-->

# 经验分布：最小方差| Quantivity

> 来源：[`quantivity.wordpress.com/2011/05/02/empirical-distribution-minimum-variance/#0001-01-01`](https://quantivity.wordpress.com/2011/05/02/empirical-distribution-minimum-variance/#0001-01-01)

交易经验提醒 Quantivity，证券收益的分布很少是[正态分布](http://en.wikipedia.org/wiki/Normal_distribution)（或[对数正态分布](http://en.wikipedia.org/wiki/Log-normal_distribution)），尽管数学上普遍假定其反之。然而，这引发了一个显而易见的问题（无论是对初学者还是专家而言）：*如果收益不是正态分布，那它们的分布又是什么*？

在[最小方差投资组合](https://quantivity.wordpress.com/2011/04/17/minimum-variance-portfolios/)（MVPs）的背景下，这个问题特别有趣，因为它们推翻了[风险溢价](https://quantivity.wordpress.com/2011/04/10/portfolio-theory-is-dead-now-what/)，并且展示了与标准股票基准相比的[显著绩效差异](https://quantivity.wordpress.com/2011/04/22/minimum-variance-sector-rotation-part-2/)。此外，试图建立对 MVP 的更高和混合阶矩的直觉，取决于对应收益分布的理解。

这篇文章分析了[经验分布](http://en.wikipedia.org/wiki/Empirical_distribution_function)来提出一个答案，而不是进行理论推测。

以下提出了两个假设。首先，*收益分布随时间变化*，既在中心矩又在形状上。换句话说，抛弃那些所有一个工具的所有收益都来自相同分布的舒适假设。其次，*忽略理论概率分布*而让数据说话。尽管交易员们不会用如此晦涩的话语，但他们不断地反响着这两种情绪。

毫不拖泥带水，考虑以下从[美国最小方差部门轮换](https://quantivity.wordpress.com/2011/04/20/minimum-variance-sector-rotation/)在 2004 年（样本中随机选择的年份）估计出的*两个*经验[概率密度函数](http://en.wikipedia.org/wiki/Probability_density_function)（PDF）的实线：

![](https://quantivity.wordpress.com/wp-content/uploads/2011/05/us-sector-2004-empiricals1.png)

这张图令人惊喜。

实线红色是标普 500 对数收益的*经验*概率密度函数（PDF）；实线黑色是最小方差投资组合对数收益的*经验*概率密度函数。为了与理论进行比较，虚线代表标准正态分布，其参数等于对应的经验分布（即均值和方差）。

换句话说，观察到的回报频率（y 轴）根据回报幅度（x 轴）绘制。经验 PDF 是通过[核密度估计](http://en.wikipedia.org/wiki/Kernel_density_estimation)（又名 Parzen 窗口）使用`density`函数估计的。由于[大数定律](http://en.wikipedia.org/wiki/Law_of_large_numbers#Weak_law)的存在，经验 PDF 收敛于实际 PDF，观测到的经验次数等于一年中的交易日（大约 250 天，对于 LLN 来说应该足够了）。

回顾一下，2004 年是一个趋势市场，SP500 收盘涨幅不到 10%。这张图的许多方面都值得注意（尤其是更高的时刻），展示了与理论的经验分歧：

+   MVP 双峰性：MVP 的 PDF 具有两个模式，几乎对称于零点的两侧（可能是两个分布的混合？）

+   MVP 厚尾：MVP 呈现的峰值比其对应的正态分布更平坦和更宽，尾部更窄。

+   SP500 负偏态：SP500 回报呈负偏态，偏度的大部分集中在（不好的）极左尾部分。

+   SP500 峰态：SP500 回报的传说中的“长尾”与相应的正态分布相比清晰可见。

+   SP500 尾部颠簸：SP500 中清晰可见两个 PDF 颠簸，在-0.01 和+0.01 处；左侧颠簸尤为令人沮丧。

所有这些观察结果都与较小方差产生的回报的*先验*直觉一致，这是由 MVP 标准优化的。更重要的是，以上观察结果表明，MVP 投资组合产生的回报应该具有相对更好的盈利表现。

现在更有趣的事情来了：考虑 MVP 和 SP500 分布之间的*估计密度差异*（计算为两个核密度函数的线性插值之间的算术差异，评估在观察到的回报范围内），并在零起点上都画上蓝线：

![](https://quantivity.wordpress.com/wp-content/uploads/2011/05/us-sector-2004-diff-empiricals.png)

这种差异密度的形状也与最小化方差一致：两个峰值说明 MVP 回报在较小值的观察频率上有相对较高的频率，对于正向和负向回报都是如此；两个低谷说明 MVP 回报在较高值的观察频率上有相对较低的频率，对于正向和负向回报都是如此。作为一个意外的惊喜，右尾中的一个小的局部极小值表明了一些大的正向惊喜。

* * *

限制分析至 2004 年，我们还未证明经验分布随时间变化的假设。现在来考虑与前面所考虑的 [美国部门轮换](https://quantivity.wordpress.com/2011/04/20/minimum-variance-sector-rotation/)（即 2000 年至 2010 年）相同的分析：

![](https://quantivity.wordpress.com/wp-content/uploads/2011/05/us-sector-annual-empiricals.png)

注意每年 *模式* 的密度的显著差异（因为所有图都使用相同的 y 轴），从 2007 年的 80 到 2002/2008/2009 年的不到 40。这清楚地说明了峰度的作用，在市场错位期间尾部急剧扩展——与 CNBC 当时喜欢大肆渲染的相对较大极端值的频率增加一致。

以及 MVP 和 SP500 之间的相同密度差异：

![](https://quantivity.wordpress.com/wp-content/uploads/2011/05/us-sector-annual-diff-empiricals.png)

为了开始解开 [全球 MVP 轮换](https://quantivity.wordpress.com/2011/04/24/minimum-variance-global-rotation/) 相对于美国部门 MVP 的相对不盈利之谜，考虑优化国际 ETF 生成的 MVP 的相应经验密度：

![](https://quantivity.wordpress.com/wp-content/uploads/2011/05/global-sector-annual-empiricals.png)

注意不同年份之间的模式存在着相同的广泛变异，差异超过 3 倍：从 2006 年的 60 到 2009 年的 20。正偏态再次发挥作用。与以上的 SPY 密度一致，2006 年、2009 年和 2010 年的全球 MVP 左尾部出现了大幅波动。最后，MVP 和 EFA 密度的形状大致更加相互一致，而不是 MVP/SPY。所有这些因素可能导致相对于美国部门的表现不佳。

以及 MVP 和 EFA 之间的相应密度差异：

![](https://quantivity.wordpress.com/wp-content/uploads/2011/05/global-sector-annual-diff-empiricals.png)

这些分布为相对于 EFA 基准的表现不佳投下了一些光。2010 年的密度在大于 0.02 的正回报上显示出显著的负差异，说明为什么 MVP 在全年的逐步下跌中比 EFA 表现更差。2009 年的大幅负峰很大程度上解释了为什么 MVP 在金融危机低点时没有超过 EFA。最后，2007 年的 MVP 有一个大的负峰，并且没有以任何正峰进行补偿。

对于有兴趣将经验分布分析进一步应用于投资组合优化的读者，他们可能希望考虑 DeMiguel 和 Nogales [2009] 的[具有鲁棒估计的投资组合选择](http://or.journal.informs.org/cgi/content/abstract/57/3/560)。

* * *

生成上述经验分布分析的 R 代码如下：

```

# empirical distributions (densities) for benchmark and MVP
quartz()
par(mfrow=c(3,4))
sapply(annualReturnNames, function (yr) { plot(density(dailyPnL[yr]), type='l', xlab="", ylab="Density", ylim=c(0,80), main=format(yr)); lines(density(diffspy[yr]), col='red'); curve(dnorm(x, mean=mean(dailyPnL[yr]), sd=sd(dailyPnL[yr])), col = 'black', add = TRUE, lty=3); curve(dnorm(x, mean=mean(diffspy[yr]), sd=sd(diffspy[yr])), col = 'red', add = TRUE, lty=3) })

# differential empirical distributions (densities)
# requires interpolation via approxfun(), as density() generates $x at different spacing
quartz()
par(mfrow=c(3,4))
sapply(annualReturnNames, function (yr) { densityX <- density(dailyPnL[yr])$x; dailyd <- density(dailyPnL[yr]); spyd <- density(diffspy[yr]); dailyFn <- approxfun(x=dailyd$x, y=dailyd$y); spyFn <- approxfun(x=spyd$x, y=spyd$y); densityDiff <- function(x) {dailyFn(x) - spyFn(x)}; diffY <- densityDiff(densityX); plot(x=densityX, y=diffY, type='l', xlab='', ylab='Density Difference', main=format(yr)); abline(h=0, v=0, col='blue') })

```

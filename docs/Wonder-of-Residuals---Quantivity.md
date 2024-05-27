<!--yml

类别：未分类

日期：2024-05-18 13:52:50

-->

# 残差的奇迹 | Quantivity

> 来源：[`quantivity.wordpress.com/2009/08/02/wonder-of-residuals/#0001-01-01`](https://quantivity.wordpress.com/2009/08/02/wonder-of-residuals/#0001-01-01)

一些数学 [构造](http://en.wikipedia.org/wiki/Construct_(philosophy_of_science)) 在交易策略中反复出现，以至于它们演变成量化交易的 [心智模型](http://en.wikipedia.org/wiki/Mental_model)。这些构造每一个都值得一篇文章，鉴于它们在算法交易中的基础作用。

残差是这些奇妙构造之一。

许多 [市场中性](http://en.wikipedia.org/wiki/Market_neutral) 策略源于残差，特别是套利家族：波动率套利、分散套利、指数套利、篮子套利、相关套利，*等等*。残差还为交易打开了一个无限大小的可投资资产宇宙，而不仅仅是从 [Yahoo](http://finance.yahoo.com) 或 [Bloomberg](http://www.bloomberg.com) 获取报价的工具。

从概念上讲，残差看起来很简单：

> 残差是样本与其对应的估计函数值之间的差异。

例如，[均值回归](https://quantivity.wordpress.com/2009/07/19/mean-reversion/) 文章估计了 2007-2008 期间 SPY 和 PRF 之间的以下线性关系：

`PRF = -7.356 + (0.455 * SPY)`

这个函数生成了给定 SPY 值时 PRF 的估计值。将其转化为交易：购买一股 PRF，做空 0.455 股 SPY，并支付 $7.356 现金。这种组合形成了一个 [篮子](http://en.wikipedia.org/wiki/Basket_(finance))（这是对经典的 [配对](http://en.wikipedia.org/wiki/Pairs_trade) 的一种概括），这是一种 *合成工具*。这种合成品可以随时在交易所买卖，就像任何传统资产一样。

鉴于这个合成品，第一个问题是如何定价的？你猜对了：合成品的价格等于残差！具体而言，等于 PRF（样本）的实际价格与方程式估算值之间的差异。具体地说，合成品的价格如下，重新排列函数以解出残差项（ε）：

`ε = PRF - (0.455 * SPY) + 7.356`

这个看似无害的方程式掩盖了奇迹，值得稍作停留：*残差定价了一种合成资产的线性组合*（以本例中的 SPY、PRF 和现金为例）。类似地，持有这一对的利润，从昨天到今天，等于将今天的残差值从昨天的值中减去。更一般地说，持有合成品的利润可以在任意两个时间 *t* 和 *t+1* 之间计算：

利润 = ε[t+1] – ε[t]

这个简单的例子暗示了一个非常深刻的泛化，归功于基本代数：对于两个或多个资产，存在无限数量的线性组合，更不用说可投资的资产宇宙（全球股票、商品、外汇以及相应的衍生品）。如果存在无限数量的线性组合，那么就会有无限数量的残差。如果有无限数量的残差，那么就会有无限数量的合成物。

换句话说，*残差为投资进入无限数量的潜在资产敞开了大门*，而不仅仅是传统可投资宇宙中的几千种。对于统计学讽刺地称为[“误差”](http://en.wikipedia.org/wiki/Errors_and_residuals_in_statistics)的小希腊字母ε来说，这是相当惊人的。

合成物只是残差的一个美妙之果。随后的*奇迹*文章将涵盖非 OLS 残差（*例如*，广义回归、状态空间模型和小波）以及使用残差选择交易的技术，在这个无限大小的投资宇宙中评估它们的稳定性，例如方差分析和[结构性变化](http://en.wikipedia.org/wiki/Structural_change) (*例如* 方差比检验、[ACF](http://en.wikipedia.org/wiki/Autocorrelation)、[Chow](http://en.wikipedia.org/wiki/Chow_test) / Quandt 检验以及迭代系数估计)。

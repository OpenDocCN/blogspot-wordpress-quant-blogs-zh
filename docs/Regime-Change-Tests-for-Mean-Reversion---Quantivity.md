<!--yml

类别：未分类

日期：2024-05-18 13:56:04

-->

# Regime Change Tests for Mean Reversion | Quantivity

> 来源：[`quantivity.wordpress.com/2009/08/15/regime-change-tests-mean-reversion/#0001-01-01`](https://quantivity.wordpress.com/2009/08/15/regime-change-tests-mean-reversion/#0001-01-01)

一位机构算法交易员最近提出了以下问题：

> 问：所以我有均值回归的数据，但然后均值发生了变化……对我而言，何时发生这种情况的最佳测试是什么？

正如 always，没有单一的“正确答案”。回答这个问题取决于对之前关于[Quantile Stability](https://quantivity.wordpress.com/2009/08/03/stability-by-quantile/)的博文的广泛概括。

适用检测方法取决于对“平均变化”的解释。在此背景下需要考虑的因素包括：

+   信号来源（类型和构建）

+   模型线性度

+   不连续性形式（线性或非线性）

+   所需的检测频率

由于参数稳定性而产生的不连续性，可以通过分析估计和分解的技巧来受益。经典的经济计量学结构变化方法（Chow、Quandt、CUSUM 等）可以用来检测低维、线性时间序列的不连续性。分位数回归可能有效地评估参数线性模型的非时间连续性/稳定性。高维、非线性时间序列的不连续性可以通过[小波](http://en.wikipedia.org/wiki/Wavelet)分解来检测。所有这些方法都可以通过使用相应的迭代算法形式，几乎在任何频率上变为伪自适应。

由于方差或协方差稳定性而产生的不连续性，可从分析协方差结构的技巧中受益。在这个领域中，有很多可供选择的技术，最常见的包括：基于方差的检验（例如，方差比[ACF](http://en.wikipedia.org/wiki/Autocorrelation_function)）、正交/正交分解技术（例如[PCA](http://en.wikipedia.org/wiki/Principal_component_analysis)或[ICA](http://en.wikipedia.org/wiki/Independent_component_analysis)）、以及[[G]ARCH 家族](http://en.wikipedia.org/wiki/GARCH)。在衍生品干扰模型中，[随机波动](http://en.wikipedia.org/wiki/Stochastic_volatility)模型是常见的。

根据方法论，读者可能希望考虑对不连续性或干扰进行建模。标准的干扰/残差模型包括诸如[状态空间模型](http://en.wikipedia.org/wiki/State_space_(controls))（如 Kalman 的线性滤波器的推广）等技术。

后续博文将深入探讨在量化交易中使用每种技术的实际应用。

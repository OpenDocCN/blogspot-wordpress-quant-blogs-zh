<!--yml

类别：未分类

日期：2024-05-18 13:55:03

-->

# 通过残差逻辑回归进行方向预测 | 量化投资

> 来源：[`quantivity.wordpress.com/2009/12/27/directional-prediction-via-residual-logistic-regression/#0001-01-01`](https://quantivity.wordpress.com/2009/12/27/directional-prediction-via-residual-logistic-regression/#0001-01-01)

Paul Teetor 写了一篇关于[预测交换价差](http://quanttrader.info/public/predictingSwapSpreads.pdf)的精彩研究。值得注意的是他使用[逻辑回归](http://en.wikipedia.org/wiki/Logistic_regression)来预测下一期价差的*概率方向*，基于从历史价差的线性模型计算的*残差*。换句话说，Paul 正在评估以下逻辑假设（从第 5 页综合而得）：

> 可以使用从具有影响力的市场数据（国库券、利率互换、LIBOR、BIX、SPX）估计的历史错定价到公平价值来预测交换价差的未来方向。

提供了稳健的方向性预测后，可以将盈利交易策略定义为（第 22 页）：

*做多*：如果 P(上涨) > 0.5，则今天做多

*简短*：如果 P(下跌) > 0.5，则今天做空

这种方法特别有趣，因为它对许多其他金融工具同样适用，只要提供了“错定价”和价值估计量的合适概念。例如，可以类似地估计协整对的方向性预测，延伸了[均值回归](https://quantivity.wordpress.com/2009/07/19/mean-reversion/)中介绍的分析。

这种方法的通用适用性来自两个方面：

+   方向性预测：逻辑回归用于估计价差上升或下降的概率，因此是*方向变化*，而不是数值。

+   残差：逻辑回归的解释变量是线性回归的残差，展示了残差的另一个[奇迹](https://quantivity.wordpress.com/2009/08/02/wonder-of-residuals/)

以下步骤概述了这种方法，以及如何将其转化为机械交易系统：

1.  估计公平价值（第 14 页）：使用交易员已知与交换价差相关的市场数据（国库券、利率互换、LIBOR、BIX、SPX）通过线性回归估计交换价差的公平价值

1.  计算“错定价”（第 16 页）：计算交换价差的观察值与估计公平价值之间的差异，生成残差序列（注意，当绘制在时间轴上时，它们表现出序列依赖性，表明它们可能具有时间上的解释能力）

1.  估计方向概率（第 19 页）：估计两个逻辑回归模型，一个用于“买入模型”，一个用于“卖出模型”，每个模型的因变量是方向概率的对数（*即*增加或减少的价差），自变量是“错定价”残差。

1.  评估重要性（第 20 页）：评估逻辑回归的![](img/e59dd600f7eb22f952e355797bceba2e.png)的重要性；如果显著，则“错定价”残差具有预测未来价差方向的能力

1.  建立交易系统（第 22 页）：提供了重要的方向预测，生成相应的多空日交易入场规则

注：对于对技术指标感兴趣的人士，保罗在他的分析中还包括动量和加速度指标（见第 6 页）。这些指标的使用与上述方法论讨论无关，因此为简洁起见，本文省略了。

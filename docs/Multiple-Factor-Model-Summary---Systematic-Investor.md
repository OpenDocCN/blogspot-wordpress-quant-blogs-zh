<!--yml

类别：未分类

日期：2024-05-18 14:42:05

-->

# 多因子模型摘要 | Systematic Investor

> 来源：[`systematicinvestor.wordpress.com/2012/03/11/multiple-factor-model-summary/#0001-01-01`](https://systematicinvestor.wordpress.com/2012/03/11/multiple-factor-model-summary/#0001-01-01)

[主页](https://systematicinvestor.wordpress.com/ "转到主页")

[因子模型](https://systematicinvestor.wordpress.com/category/factor-model/)

，

[因素](https://systematicinvestor.wordpress.com/category/factors/)

> 多因子模型摘要

## 多因子模型摘要

在这篇文章中，我想总结我在多因子模型系列中涵盖的所有材料。 [多因子模型](http://www.investopedia.com/terms/m/multifactor-model.asp) 可用于分解收益和计算风险。 以下是一些多因子模型的示例：

模型中的因素通常使用定价、基本、分析师估计和专有数据创建。 我将仅展示使用定价和基本数据的因素示例，因为这些信息可以轻松从 Yahoo Finance 和 ADVFN 获取。

以下是我写的关于多因子模型的所有帖子的摘要：

1.  [多因子模型 - 基本数据](https://systematicinvestor.wordpress.com/2012/01/29/multiple-factor-model-fundamental-data/) - 在这篇文章中，我演示了如何将公司的基本数据导入 R，创建一个简单的因子，并运行相关分析。

1.  [多因子模型 - 构建基本因子](https://systematicinvestor.wordpress.com/2012/02/04/multiple-factor-model-building-fundamental-factors/) - 在这篇文章中，我演示了如何构建 CSFB Alpha Factor Framework 中描述的基本因子，并计算分位差。 有关 CSFB Alpha Factor Framework 的详细信息，请阅读[CSFB 量化研究，第 11 页，第 49 页，由 P. N. Patel，S. Yao，R. Carlson，A. Banerji，J. Handelman 编写](http://www.scribd.com/mobile/documents/62210581/download?commit=Download+Now&secret_password=)。

1.  [多因子模型 - 构建 CSFB 因子](https://systematicinvestor.wordpress.com/2012/02/13/multiple-factor-model-building-csfb-factors/) - 在这篇文章中，我演示了如何构建 CSFB Alpha Factor Framework 中描述的大多数因子，运行横截面回归以估计因子载荷，创建和测试 Alpha 模型。

1.  [多因子模型 - 构建风险模型](https://systematicinvestor.wordpress.com/2012/02/21/multiple-factor-model-building-risk-model/) - 在这篇文章中，我演示了如何构建多因子风险模型，使用收缩估计器计算因子协方差，使用 GARCH(1,1)预测股票特定方差。

1.  [投资组合优化——为什么我们需要风险模型](https://systematicinvestor.wordpress.com/2012/02/26/portfolio-optimization-why-do-we-need-a-risk-model/) – 在这篇文章中，我解释了为什么我们需要风险模型，并展示了它在投资组合构建过程中的使用方法。

1.  [多因子模型——构建 130/30 指数](https://systematicinvestor.wordpress.com/2012/03/06/multiple-factor-model-building-13030-index/) – 在这篇文章中，我展示了如何基于我们之前创建的 CSFB 因子和风险模型构建 130/30 指数。A. Lo 和 P. Patel 的[论文](http://math.nyu.edu/faculty/avellane/Lo13030.pdf)详细介绍了如何使用平均 CSFB 因子作为 alpha 模型以及[MSCI Barra 多因子风险模型](http://www.alacra.com/alacra/help/barra_handbook_US.pdf)构建 130/30 指数。

1.  [多因子模型——构建 130/30 指数（更新）](https://systematicinvestor.wordpress.com/2012/03/10/multiple-factor-model-building-13030-index-update/) – 在这篇文章中，我展示了如何构建市场中性策略和最小方差策略，并将它们的表现与 130/30 指数进行比较。

在 Pat Burns 的[文章](http://www.portfolioprobe.com/2012/01/05/the-top-7-portfolio-optimization-problems/)中，对投资组合构建问题及其可能的解决方案进行了出色的讨论。我想强调两个与多因子模型相关的问题。

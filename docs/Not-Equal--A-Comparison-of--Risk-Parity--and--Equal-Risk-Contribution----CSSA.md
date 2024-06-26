<!--yml

分类：未分类

日期：2024-05-12 18:05:44

-->

# 不等同：风险平价与等风险贡献的比较 | CSSA

> 来源：[`cssanalytics.wordpress.com/2012/07/19/not-equal-a-comparison-of-risk-parity-and-equal-risk-contribution/#0001-01-01`](https://cssanalytics.wordpress.com/2012/07/19/not-equal-a-comparison-of-risk-parity-and-equal-risk-contribution/#0001-01-01)

**“风险平价”**这个术语经常令人困惑，因为它根据公司不同而有不同的定义和应用。随着战术资产配置和指数化策略的多种变化的出现，或许可以声称风险平价与用“对冲基金”这个术语来描述一种投资管理风格一样模糊和难以捉摸。我下面创建了一个表格，以澄清两个经常可以互换使用但*不是*相同的变体。  关于风险平价起源的良好历史可以在这里找到：[`en.wikipedia.org/wiki/Risk_parity`](http://en.wikipedia.org/wiki/Risk_parity)。**系统投资者**——一个优秀的博客——在这里提供了一些有用的 R 代码和测试：[`systematicinvestor.wordpress.com/2012/03/19/backtesting-asset-allocation-portfolios/`](http://systematicinvestor.wordpress.com/2012/03/19/backtesting-asset-allocation-portfolios/ "风险平价在 R 中")。**梅班·法伯**——总是为新想法提供极好的资源——在这里提供了将风险平价应用于资产分配的应用，以及一份很好的文章列表：[`www.mebanefaber.com/2012/03/22/risk-parity-vs-endowment-model-vs-permanent-portfolio/`](http://www.mebanefaber.com/2012/03/22/risk-parity-vs-endowment-model-vs-permanent-portfolio/ "法伯风险平价")

在我看来，将**风险平价**视为一个广泛的风险预算方案类别最为简单。在这个类别中，投资组合中每个资产的风险（如有必要）都会被杠杆化，以拥有相同的波动性。本质上，每个资产都具有“平等的风险”，因此，由于回报和风险较少依赖于任何一个资产，投资组合被认为是更加多元化的。相比之下，**罗纳尔迪** [`www.thierry-roncalli.com/riskparity.html`](http://www.thierry-roncalli.com/riskparity.html "罗纳尔迪") 提出了**“等风险贡献”（ERC）**这一术语，它是**风险平价的一个独立子类别**，旨在使每个资产对投资组合的风险贡献相等。如果阅读了各种文章之后，这两种方法听起来相同，那是因为在经常引用的两资产案例中，它们有相同的数学解决方案和解释其有效性的原因。然而，并非所有的风险平价投资组合都是一样的——理解等风险与等风险贡献方法之间的差异，以避免不当的应用或解释是必要的。下面是一个表格，有助于定义这两种方法的相似之处和不同之处，以及每种方法在投资组合分配中的相对优势。

**等风险贡献（ERC）和风险平价（RP）共享的特点和品质**

| **算法特点** | **等效性** | **等风险贡献（ERC）** | **风险平价（RP）** |
| --- | --- | --- | --- |
| 需要历史/预期资产回报 | ≈ | 无 | 无 |
| 被认为是缺乏强理论支持的启发式算法 | ≈ | 是 | 是 |
| 通常使用杠杆 | ≈ | 是 | 是 |
| 通常使用目标组合风险 | ≈ | 是 | 是 |
| 在所选宇宙中的所有资产分配 | ≈ | 是 | 是 |
| 相对于传统模型，换手率较低 | ≈ | 是 | 是 |
| 与传统模型相比，对估计误差的敏感性相对较低 | ≈ | 是 | 是 |
| 通常比等权重组合具有更高的回报和夏普比率 | ≈ | 是 | 是 |
| 比 60/40 平衡股票/债券组合具有更好的回报和夏普比率 | ≈ | 是 | 是 |
| 二资产组合的解决方案 | ≈ | 波动率倒数的加权 | 波动率倒数的加权 |
| 与等权重组合等效的条件 | ≈ | 资产波动率相等且相关系数恒定 | 资产波动率相等且相关系数恒定 |
| 在有效前沿上最优的条件 | ≈ | 夏普比率相等且相关系数恒定 | 夏普比率相等且相关系数恒定 |

**有利于等风险贡献（ERC）的特点和品质**

| **算法特点** | **等效性** | **等风险贡献（ERC）** | **风险平价（RP）** |
| --- | --- | --- | --- |
| 目标函数 | ≠ | 风险贡献的波动率=0 | 波动率倒数的加权 |
| 使用贝塔/协方差数据 | ≠ | 是 | 无 |
| 总是假设恒定的相关系数矩阵 | ≠ | 无 | 是 |
| 持仓的风险贡献对组合波动率相等 | ≠ | 是 | 无 |
| 性能对所选资产组合的宇宙非常敏感 | ≠ | 无 | 是（例如，5 只股票和 1 只债券会产生不平衡） |
| 用于风险预算和因子倾斜的灵活性 | ≠ | 胜者 | 败者 |
| 样本外风险（给定相同的目标） | ≠ | 胜者 | 败者 |
| 在样本外回报（给定相同的目标或杠杆约束） | ≠ | 胜者 | 败者 |
| 样本外回撤 | ≠ | 胜者 | 败者 |
| 样本外夏普比率 | ≠ | 胜者 | 败者 |
| 样本外多样化（集中度和平均相关性） | ≠ | 胜者 | 败者 |
| 有利的混合方法，介于最小方差和等权重之间 | ≠ | 是 | 无 |
| 可以与最小方差等效 | ≠ | 当相关系数矩阵最小时 | 不可能 |

**有利于风险平价（RP）或等风险的特点和品质**

| **算法特点** | **等效性** | **等风险贡献（ERC）** | **风险平价（RP）** |
| --- | --- | --- | --- |
| 对数学能力弱的人来说简单易算（餐巾纸因子） | ≠ | 败者 | 胜者 |
| 直观容易理解并在大多数软件包中使用 | ≠ | 无 | 是 |
| 最佳发音名称/酷因素 | ≠ | 败者 | 胜者 |
| 使用长期月度数据进行动态分配的实用方法 | ≠ | 败者 | 胜者 |
| 对协方差估计误差的敏感性 | ≠ | 输家 | 赢家 |
| 通常需要一个复杂的求解器进行优化 | ≠ | 是 | 否 |
| 对大量宇宙计算的速度 | ≠ | 慢 | 快 |
| 在有限样本量下处理非常大数据集的表现 | ≠ | 输家（相对于样本量，协方差太多） | 赢家（相对于样本量，要估计的变量较少） |

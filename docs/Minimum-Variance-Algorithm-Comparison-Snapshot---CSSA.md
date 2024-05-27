<!--yml

分类：未分类

日期：2024-05-12 18:00:23

-->

# 最小方差算法比较快照 | CSSA

> 来源：[`cssanalytics.wordpress.com/2013/04/19/minimum-variance-algorithm-comparison-snapshot/#0001-01-01`](https://cssanalytics.wordpress.com/2013/04/19/minimum-variance-algorithm-comparison-snapshot/#0001-01-01)

**最小方差算法**（Minimum Variance Algorithm，MVA）与几种标准优化方法和算法在最近一组测试中进行了比较，这些测试由[Systematic Investor](http://systematicinvestor.wordpress.com/)的 Michael Kapler 进行。Michael 创建了一个关于 MVA 的[网页](http://www.systematicportfolio.com/minvar)，以回顾这些测试的一些细节，并总结一些背景信息。我们计划在未来的几周内发布一份关于 MVA 的白皮书，其中包含一些附加材料。以下是包含在[最小相关性算法](https://cssanalytics.wordpress.com/2012/09/21/minimum-correlation-algorithm-paper-release/)论文中的多组测试的摘要。我们使用了一个标准化的分数（z-分数的 normsdist），用于衡量每种方法与其他方法的性能——使用三个指标：1）夏普比率（越高越好）2）波动性（越低越好）3）组合换手率（越低越好）。这些因素被平等地加权，以创建一个综合分数。我们在一个广泛的数据集上进行了测试——股票、ETF 和期货。在所有方法中，**最小方差算法**（在下图中的 MVE）的得分最高，优于标准的**最小方差算法**以及[最小相关性算法](https://cssanalytics.wordpress.com/2012/09/27/minimum-correlation-implementation-in-excel/)。

![mva summary](https://cssanalytics.files.wordpress.com/2013/04/mva-summary.png)

以下缩写定义见下文。

**MVE**：**最小方差算法**（MVA）在 Excel 中

**MCE**：最小相关性算法（MCA）在 Excel 中

**MC**：最小相关性算法（MCA）–白皮书/R 版本

**MC2**：最小相关性算法 2（MCA）

**MV**：最小方差——使用二次优化器的长仓标准最小方差

**MD**：最大多样化–使用二次优化器的长仓标准多样化

**EW**：等权重

**RP**：风险平价——基本版本，反波动性加权

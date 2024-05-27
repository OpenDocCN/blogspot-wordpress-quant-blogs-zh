<!--yml

分类：未分类

日期：2024 年 05 月 12 日 18:02:51

-->

# 一种优雅的多样化衡量方法：聚类基尼分数（CGS）| CSSA

> 来源：[`cssanalytics.wordpress.com/2013/01/09/an-elegant-measure-of-diversification-the-cluster-gini-score-cgs/#0001-01-01`](https://cssanalytics.wordpress.com/2013/01/09/an-elegant-measure-of-diversification-the-cluster-gini-score-cgs/#0001-01-01)

在我们撰写的关于[最小相关算法](https://cssanalytics.wordpress.com/2012/09/12/minimum-correlation-algorithm-mca/ "Minimum Correlation Algorithm (MCA)")的论文中，我们介绍了复合多样化评分（CDI）。这一措施的目的是展示一组投资组合权重如何最小化平均投资组合相关性，并且平衡每个资产的风险贡献，使用[基尼](https://cssanalytics.wordpress.com/2012/10/22/gini-calculation-spreadsheet/ "Gini Calculation Spreadsheet")系数进行衡量不平等。当应用于集群时，CDI 也可以类似地扩展到 CGS-这超出了本文的范围。

一种替代性且潜在更直观的投资组合多样化衡量方法使用了[集群风险平价](https://cssanalytics.wordpress.com/2013/01/03/cluster-risk-parity/ "Cluster Risk Parity") (CRP)中蕴含的概念。逻辑非常简单：如果 CRP 使用 ERC（等风险贡献）在集群内部和跨集群中都代表“最优多样化投资组合”，那么任何偏离这一点的投资组合都被认为在风险/多样化方面存在不同程度的不平衡。实质上，来自给定宇宙的投资组合被认为对每个集群都有“因子”敞口，并且对这些因子也有“跟踪误差”（跑输基准的风险）。在实践中，我们希望在因子/集群风险之间实现风险的平衡，以及对因子/集群敞口的风险进行平衡。Gini 系数被用于 CDI 中度量风险贡献敞口的不平等性。一种度量方式是(1-Gini)资产风险贡献的情况下，值为 1 代表完美平等，0 代表完美不平等。相同的概念可以扩展到跨（间）因子/集群风险贡献和内部（内）因子/集群风险贡献。CGS 的公式如下：

***CGS=  100x (sqrt(NC)x(inter-cluster RC (1-Gini))+(avg intra-cluster RC (1-Gini)))/(sqrt(NC)+1)***

本质上，这是对因子风险平衡的加权，与平均因子内风险平衡相比，跨因子（跨集群）被分配了更大的权重，该权重是可用集群数量的平方根的函数。 结果方程显示结果介于 0 和 100 之间，其中 100 是集群风险平衡配置，而非常低的分数表示高度集中和风险分配不佳。 此分数可用于确定在给定宇宙中的任何一组投资组合权重的分散/集中程度。 换句话说，如果你例如有 5 个资产和一组你认为是最佳的权重，CGS 可以帮助确定你在分散化方面的不平衡程度。 这也可以扩展到优化，其中 CGS 可以帮助调节目标函数以确保更稳定的结果，并生成更直观的投资组合。 在机器学习算法和数据挖掘中，CGS 可以帮助生成更稳定的预测，并增强在使用聚类时处理大型数据集的能力。

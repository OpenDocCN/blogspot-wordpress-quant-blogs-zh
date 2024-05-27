<!--yml

类别：未分类

日期：2024-05-12 18:02:31

-->

# 使用动态聚类与常规风险平价方法进行回溯测试|CSSA

> 来源：[`cssanalytics.wordpress.com/2013/01/11/a-backtest-using-dynamic-clustering-versus-conventional-risk-parity-methods/#0001-01-01`](https://cssanalytics.wordpress.com/2013/01/11/a-backtest-using-dynamic-clustering-versus-conventional-risk-parity-methods/#0001-01-01)

这是一个使用[动态聚类方法](http://systematicinvestor.wordpress.com/2012/12/29/clustering-with-selected-principal-components/)进行的回溯测试，该方法由[Systematic Investor](http://systematicinvestor.wordpress.com/)的 Michael Kapler 引入，并结合了多种配置方案：1）**在和跨集群内均衡分配** 2）**在和跨集群内风险平价** 和 3）**[集群风险平价](https://cssanalytics.wordpress.com/2013/01/03/cluster-risk-parity/ "Cluster Risk Parity") (CRP)：** 在和跨集群内使用等风险贡献（ERC）。为了比较，我们展示了等权重配置、[风险平价和风险平价 ERC](https://cssanalytics.wordpress.com/2012/07/19/not-equal-a-comparison-of-risk-parity-and-equal-risk-contribution/ "Not Equal: A Comparison of “Risk Parity” and “Equal Risk Contribution”") 而没有进行聚类。在测试中，我们使用了 10 个主要资产类别的 ETF。  

![etfs 上的集群](https://cssanalytics.files.wordpress.com/2013/01/cluster-on-etfs.png)

对于动态聚类版本的平均表现与其非聚类对应版本的平均表现相比，在回报和风险调整基础上略有优势。所有单独的聚类方法也优于其非聚类对应方法。更重要的是，风险平价聚类（CRP）–或风险平价 ERC 的动态聚类–是最佳表现者，并且在风险调整回报方面优于所有其他配置方法，并且具有第二高的年化回报。这只是一个宇宙，差异并不显著–但符合我们在理论上的预期。有许多移动的部分–聚类方法和输入（方差/协方差信息和回报）都可以用来改善性能并减少周转。但是最基本的方法往往表明了这种理论方法的有效性。在下一篇文章中，我们将在不同的宇宙中研究静态与动态聚类的比较。

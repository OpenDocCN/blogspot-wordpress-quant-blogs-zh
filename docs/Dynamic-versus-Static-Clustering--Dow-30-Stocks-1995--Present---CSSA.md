<!--yml

category: 未分类

date: 2024-05-12 18:02:17

-->

# Dynamic versus Static Clustering: Dow 30 Stocks 1995- Present | CSSA

> 来源：[`cssanalytics.wordpress.com/2013/01/14/dynamic-versus-static-clustering-dow-30-stocks-1995-present/#0001-01-01`](https://cssanalytics.wordpress.com/2013/01/14/dynamic-versus-static-clustering-dow-30-stocks-1995-present/#0001-01-01)

一个自然的比较对象是使用[动态聚类](https://cssanalytics.wordpress.com/2013/01/11/a-backtest-using-dynamic-clustering-versus-conventional-risk-parity-methods/ "使用动态聚类与传统风险平价方法进行回测")的配置方法，与使用静态聚类方法相比。 静态聚类的一个示例是由大型指数公司进行的部门分类。 通常，根据与公司相关联的业务或行业类型形成集群（即公用事业，能源等）。 道琼斯工业平均指数包含有着非常长的交易历史的 30 只大市值股票。此外，每只股票都可以根据其各自的[S&P 部门](http://www.sectorspdr.com/)轻松分类。这种静态聚类也可以作为合并[风险平价](https://cssanalytics.wordpress.com/2012/07/19/not-equal-a-comparison-of-risk-parity-and-equal-risk-contribution/ "不相等：风险平价和等风险贡献的比较")方法的基础，用于投资组合配置。以下测试由**迈克尔·卡普勒**在**[Systematic Investor](http://systematicinvestor.wordpress.com/)**使用[主成分](http://systematicinvestor.wordpress.com/2012/12/29/clustering-with-selected-principal-components/)进行动态聚类时在 R 中进行。

![道琼斯 30 指数聚类](https://cssanalytics.files.wordpress.com/2013/01/dow-30-clusters.png)

你可以看到，动态聚类比静态聚类具有一小但一致的优势。动态方法在长期回溯期间产生了更高的回报和风险调整后的回报。再次，[集群风险平价](https://cssanalytics.wordpress.com/2013/01/06/cluster-risk-parity-crp-versus-risk-parity-rp-and-equal-risk-contribution-erc/ "集群风险平价 (CRP) 对风险平价 (RP) 和等风险贡献 (ERC) 的比较")（使用风险平价或风险平价-erc 的动态聚类）比任何其他风险平价变体表现更好。此外，**动态聚类也比非聚类方法产生更好的回报和风险调整后的回报**。有趣的是，静态聚类并不像完全忽略集群那样有效。这表明，变化的波动率和相关性包含了可以在动态基础上利用的信息。这一发现在波动率方面是直观的——波动率是高度可预测的——但对于那些认为相关性无用的批评者可能会感到惊讶。事实上，观察等权动态聚类与普通等权仅仅的动态贡献，表明它们对于这个数据集的超额表现贡献最大。这是合理的，考虑到大多数股票具有类似的波动率，但它们的相关性可能是时变的。

虽然这个测试并不是决定性的——它再次支持了一个逻辑和理论上的结论，即在投资组合配置的动态方法中，聚类是有价值的。它还表明，动态聚类是静态聚类的一种可行替代——静态聚类很麻烦，可能没有对于给定的股票或资产组合的先例。动态聚类的有用性与静态聚类相比取决于距离度量的可预测性——在这种情况下，样本相关性。虽然我同意相关性可能会有噪音并且需要被稳定，但如果有合理的预期可以对其进行预测，那么最好尝试合并可能有用的信息，而不是完全忽略这些信息。可以始终改进相关性预测或使用不同的距离度量集合。

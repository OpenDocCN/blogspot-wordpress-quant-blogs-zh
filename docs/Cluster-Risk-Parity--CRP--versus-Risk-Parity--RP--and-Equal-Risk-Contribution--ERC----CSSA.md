<!--yml

类别：未分类

日期：2024-05-12 18:03:07

-->

# 集群风险平价（CRP）与风险平价（RP）和等风险贡献（ERC） | CSSA

> 来源：[`cssanalytics.wordpress.com/2013/01/06/cluster-risk-parity-crp-versus-risk-parity-rp-and-equal-risk-contribution-erc/#0001-01-01`](https://cssanalytics.wordpress.com/2013/01/06/cluster-risk-parity-crp-versus-risk-parity-rp-and-equal-risk-contribution-erc/#0001-01-01)

[集群风险平价](https://cssanalytics.wordpress.com/2013/01/03/cluster-risk-parity/ "Cluster Risk Parity")（*Varadi, Kapler, 2012*）是一种改进 [风险平价和等风险贡献](https://cssanalytics.wordpress.com/2012/07/19/not-equal-a-comparison-of-risk-parity-and-equal-risk-contribution/ "Not Equal: A Comparison of “Risk Parity” and “Equal Risk Contribution”") 不足的方法：a）需要手动选择宇宙（参见 [全天候和永久组合](https://cssanalytics.wordpress.com/2012/11/07/the-all-weather-portfolio-derivation/ "The “All-Weather” Portfolio Derivation"））；b）所选宇宙的风险暴露不平衡。为了突出后一问题，值得看一个例子，我们只使用标准普尔 500（SPY）和国库券（TLT）时间序列来创建投资组合的宇宙。这个例子不是那么极端，因为习惯上包括代表多个部门或国家的多个 ETF 或共同基金以及与多个债券 ETF/基金一起包含的多个债券 ETF/基金。  过去一年的数据使用以下示例非常重要：

![CRP](https://cssanalytics.files.wordpress.com/2013/01/crp.png)

这个分析的要点是，债券与股票的数量或组合将极大地影响投资组合的风险贡献，而传统的风险平价方法。 在上述例子中，即使只考虑 5 种资产情况，风险的扭曲也是显著的-风险平价中超过 100%的风险来自股票，而 ERC 中高达 80%的风险来自股票。 相比之下，集群风险平价（CRP）无论宇宙的数量或组合如何都是平衡的。 这有助于确保风险管理和绩效的一致性，并确保投资组合再平衡产生预期的影响。 使用手动编译/分类，比如说“股票”或“债券”，不足以避免这个问题，因为有时存在交叉（比如高收益），而且当相关性低时，每个类别内部甚至存在显著差异。 使用 CRP 是避免这些问题的最简单方法，而无需进行大量的临时分析和持续进行调整。

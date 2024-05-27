<!--yml

分类：未分类

日期：2024-05-12 17:48:23

-->

# 百分位通道策略复制 | CSSA

> 来源：[`cssanalytics.wordpress.com/2015/02/16/percentile-channel-strategy-replication/#0001-01-01`](https://cssanalytics.wordpress.com/2015/02/16/percentile-channel-strategy-replication/#0001-01-01)

迈克尔·卡普勒（Michael Kapler）是始终卓越的[系统投资者](https://systematicinvestor.wordpress.com/)博客的作者，他已经将他的发布移至 GitHub，以使发布代码变得更加容易。这一变化并未引起太多关注（甚至没引起我的注意），我们都很感激他重新开始发布内容。他能够在最近的一篇博文中复现[百分位通道策略](https://cssanalytics.wordpress.com/2015/01/26/a-simple-tactical-asset-allocation-portfolio-with-percentile-channels/ "一个使用百分位通道的简单战术资产分配组合")，该博文链接[在此](http://systematicinvestor.github.io/Channel-Breakout2/)。

下表比较了原始策略（channel rp）与其他包括 1)ew- 平等权重组合中的资产 2)rp- 使用组合中的资产进行风险对等 3)channel ew: 使用平等权重进行百分位通道 TAA 策略 4)QATAA- 该策略是应用梅班·法伯（Mebane Faber）在其著名论文中提到的趋势跟踪策略（在这种情况下，QATAA 使用与百分位 TAA 策略相同的底层资产和现金分配）。当然，QATAA 是策略框架的一个灵感来源，梅班总是在他的[世界贝塔博客](http://mebfaber.com/)上发布有趣的想法。为了避免不同数据源扩展的问题，**系统投资者从 2010 年开始使用底层 ETF 数据进行测试**，以展示策略在当前牛市中的表现。如果您得到的结果与这个测试一致，那么您可以放心您有正确的细节- 否则您可以使用 R 和系统投资者在博文中提供的代码。

![通道策略复制](https://cssanalytics.files.wordpress.com/2015/02/channel-strategy-replication.png)

在比较结果后，迈克尔和我展示了一个几乎相同的匹配（我也得到了 1.42 的夏普比和 8.93%的复合年化增长率）——在最初的帖子引起的所有骚动之后，这让人松了一口气（这在我的现在觉得好笑的抱怨中有所体现，[链接](https://cssanalytics.wordpress.com/2015/02/08/a-simple-tactical-asset-allocation-portfolio-with-percentile-channels-for-dummies/ "A “Simple” Tactical Asset Allocation Portfolio with Percentile Channels (for Dummies)")）。原始策略是这一组中表现最好的，因为它同时应用了多个时间框架以及通过风险对冲进行标准化的投注大小（大多数趋势追踪者都会这样做）。正如我之前所说，我喜欢百分位通道方法的一个原因是因为这些信号可能与大多数资产经理和投资者使用的信号略有不同。

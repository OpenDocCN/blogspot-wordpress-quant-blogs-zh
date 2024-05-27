<!--yml

category: 未分类

日期：2024 年 5 月 18 日 13:52:10

-->

# 最小方差的全球轮换 | Quantivity

> 来源：[`quantivity.wordpress.com/2011/04/24/minimum-variance-global-rotation/#0001-01-01`](https://quantivity.wordpress.com/2011/04/24/minimum-variance-global-rotation/#0001-01-01)

在资产分配中分析外国股权倾向一直是宏观经济的投机，考虑到地缘政治动荡、[汇率风险](http://en.wikipedia.org/wiki/Currency_risk)和国家部门集中。为了消除自主预测，本文应用于[EAFE](http://en.wikipedia.org/wiki/MSCI_EAFE)内突出的股票市场的[最小方差轮换](https://quantivity.wordpress.com/2011/04/20/minimum-variance-sector-rotation)。结果与之前对美国部门的[1999 – 2010 年分析](https://quantivity.wordpress.com/2011/04/22/minimum-variance-sector-rotation-part-2/)进行了有趣的比较。

以下国际交易所交易基金包括在本分析中：德国（EWG），中国（FXI），巴西（EWZ），日本（EWJ），澳大利亚（EWA），韩国（EWY），意大利（EWI），法国（EWQ），加拿大（EWC），瑞典（EWD），墨西哥（EWW），和台湾（EWT）。尽管今天存在很多其他国际 ETF，但它们的成立日期太近，无法提供足够长的纵向面板。全球轮换将以[EAFE](http://en.wikipedia.org/wiki/MSCI_EAFE)作为基准（通过[EFA](http://finance.yahoo.com/q?d=t&s=EFA)），就像标准普尔 500 针对美国市场的 SPY 一样。

作为宏观经济背景，根据[IMF](http://en.wikipedia.org/wiki/International_Monetary_Fund)的[国内生产总值](http://en.wikipedia.org/wiki/Gross_domestic_product)的降序排名，全球排名前 20 的国家是：美国、中国、日本、印度、德国、俄罗斯、英国、巴西、法国、意大利、墨西哥、韩国、西班牙、加拿大、印度尼西亚、土耳其、澳大利亚、台湾、伊朗、波兰。因此，所选的 ETF 代表了排名前 20 的国家中的 12 个。它们在此期间的表现，根据对数收益，如下：

![](https://quantivity.wordpress.com/wp-content/uploads/2011/04/global-rets.png)

所有国家都在呼应金融泡沫，但后经济低谷复苏的幅度差异很大：巴西、澳大利亚、韩国、瑞典、墨西哥、加拿大和台湾，在 2010 年结束时都接近金融泡沫前的顶峰；而中国、日本、法国、德国和意大利的复苏则更为缓和。这暗示了复苏强度和 GDP 的关系：*随着 GDP 的增长，金融泡沫后的复苏逐渐减弱*。这是出人意料的，因为美国市场经历了强劲的复苏，距离金融泡沫前的顶峰仅有 15%。

市场因素解释的方差比例显著，在 2008 – 2010 年间超过了 80%。上升趋势与美国部门相似。

![](https://quantivity.wordpress.com/wp-content/uploads/2011/04/longitudinal-pca-decomp-global.png)

接下来，将从每年生成的[最小方差投资组合](https://quantivity.wordpress.com/2011/04/17/minimum-variance-portfolios/)中获取的全球权重进行可视化。 显著地，*日本的权重从不到 20%跳升至超过 100%*，与之相应的，意大利大幅减少：

![](https://quantivity.wordpress.com/wp-content/uploads/2011/04/annual-mv-global-weights1.png)

毫无疑问，日本在 2009 年和 2010 年权重支配的剧烈变化是一个值得进一步研究的谜题。 正如下文所示，这种权重变化导致了 2008 年后相当显著的制度变化。

根据这些权重推导的交易策略的每日 P＆L 表现如下：

![](https://quantivity.wordpress.com/wp-content/uploads/2011/04/mvp-pl-global.png)

显然，P＆L 非常乏味：2006 年至 2009 年略胜于基准（包括在低谷时稳定 20%的超额业绩）； 而在 2009 年中期全面崩溃。 查看日本的 2009 年回报率和 2009 年 MVP 权重，EWJ 可能应该为此负责。 考虑到 EWJ 自 2009 年 4 月以来已经在大约 10 左右均衡回归，这引发了一个方差惩罚的问题：*是否使用协方差矩阵不公平地惩罚了“好”（上行）方差，而以“坏”（下行）方差为代价*？ 或许这个问题值得进一步分析（参见[下行风险度量的简史](http://citeseer.ist.psu.edu/viewdoc/summary?doi=10.1.1.22.262)，Nawrocki [1999]）。

美国和全球轮换之间的 P＆L 显着差异值得进一步调查。 从`最小方差轮换：Part 2`（由[最小方差轮换：Part 2](https://quantivity.wordpress.com/2011/04/22/minimum-variance-sector-rotation-part-2/)定义）开始，说明其与美国市场的不一致性：*市场危机期间类似的业绩, 但市场强劲期间表现不佳*。 虽然这在定性上与最小化上行方差一致（见上文），但表现不佳的幅度是意外地显著的。

![](https://quantivity.wordpress.com/wp-content/uploads/2011/04/min-var-alpha-global.png)

α和基准的一阶差分重叠时间序列在美国行业也表现出不一致：尽管异方差性相似，但α方差在 2008 年及之后 *更一致且不那么时间同步*。相对较小的异方差性非常有趣，要求在美国与全球市场之间的α分布不同。鉴于 2008 年及之后美国和全球市场回报时间序列的定性相似性，这一观察尤为引人注目。

![](https://quantivity.wordpress.com/wp-content/uploads/2011/04/min-var-alpha-diff-global.png)

要进一步调查，考虑所有外国市场之间的平均相关性：几乎单调递增，峰值稳定在 80%以上。这种单调性与美国行业相关性形成鲜明对比，后者在 2006 年和 2009 年有所下降：

![](https://quantivity.wordpress.com/wp-content/uploads/2011/04/mean-global-correlation.png)

最后，尽管全球市场相关性增加，但α-EFA 相关性也与美国行业表现出不一致；具体来说，只有外国市场在 2009 年出现了相关性下降。

![](https://quantivity.wordpress.com/wp-content/uploads/2011/04/alpha-efa-correlation.png)

毫无疑问，这篇帖子阻止了使用最小方差进行全球轮换交易。突出问题是 *为什么*，尽管这种方法在美国部门取得成功。对此提出的几个好奇点进行进一步调查可能有助于解开这个谜团。

有什么想法吗？

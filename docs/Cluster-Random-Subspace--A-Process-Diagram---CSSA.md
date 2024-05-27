<!--yml

category: 未分类

日期：2024-05-12 17:51:41

-->

# 集群随机子空间- 过程图 | CSSA

> 来源：[`cssanalytics.wordpress.com/2014/11/05/cluster-random-subspace-a-process-diagram/#0001-01-01`](https://cssanalytics.wordpress.com/2014/11/05/cluster-random-subspace-a-process-diagram/#0001-01-01)

在上一篇文章中，我介绍了一种改进投资组合优化的方法，称为[集群随机子空间方法](https://cssanalytics.wordpress.com/2014/11/04/cluster-random-subspace-method-for-portfolio-management/ "用于投资组合管理的集群随机子空间方法")（CRSM）。该论文是由计算机科学硕士迈克尔·关撰写的，如果你错过了，可以在这里找到论文链接：[CRSM Thesis](https://cssanalytics.files.wordpress.com/2014/11/crso-thesis1.pdf)。CRSM 在大规模或同质宇宙中表现出了明显的优势，尤其是与使用传统的 Markowitz 最大夏普（MSR）投资组合相比。这是可以预料的，因为 CRSM 旨在通过聚合或使用统计集合方法来减少方差。在这些情况下，传统的 MSR 受到“[维度灾难](https://cssanalytics.wordpress.com/2013/10/03/mean-variance-optimization-and-statistical-theory/ "均值-方差优化与统计理论")”的困扰，往往更像是“误差最大化器”，而不是产生有效的投资组合配置。由于本文中使用 MSR 来最大化投资组合夏普比率，因此可以直接将其与使用标准 MSR 方法以及使用 RSM/[RSO](https://cssanalytics.wordpress.com/2013/10/10/rso-mvo-vs-standard-mvo-backtest-comparison/ "RSO MVO vs Standard MVO Backtest Comparison")（原始随机子空间方法，也使用 MSR）和等权重投资组合进行比较。CRSM-R 只是使用替换在抽样过程中的 CRSM 的变体。我从论文中取得了这张图表，汇总了使用每种算法类型的六个不同宇宙的结果。如果想更深入地了解，请阅读原始论文：

![sharpe agg crsm](https://cssanalytics.files.wordpress.com/2014/11/sharpe-agg-crsm.png)

就目标函数而言- 最大化夏普比率- CRSM 在论文中测试的宇宙中是迄今为止最好的算法，远远优于 MSR。虽然我不想泄露惊喜，但这并不是以减少的 CAGR 为代价的- 这在 Michaud 重抽样等情况下通常是这样的。事实上，CRSM 还具有最高的 CAGR- 战胜了等权重，这在同质宇宙中尤为令人印象深刻。要更好地了解 CRSM 的工作原理，可以查看下面的过程图：

![crsm2](https://cssanalytics.files.wordpress.com/2014/11/crsm2.png)

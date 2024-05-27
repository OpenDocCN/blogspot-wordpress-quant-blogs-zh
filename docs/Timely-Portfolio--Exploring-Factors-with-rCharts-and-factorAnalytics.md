<!--yml

类别：未分类

日期：2024-05-18 14:54:00

-->

# 及时组合：使用 rCharts 和 factorAnalytics 探索因子

> 来源：[`timelyportfolio.blogspot.com/2014/04/exploring-factors-with-rcharts-and.html#0001-01-01`](http://timelyportfolio.blogspot.com/2014/04/exploring-factors-with-rcharts-and.html#0001-01-01)

Fama 和 French 在 1993 年用他们的[因子](http://scholar.google.com/scholar?cluster=12390788233497435001&hl=en&as_sdt=0,1)改变了金融世界。另一对搭档 Andrea Frazzini 和 Lasse Heje Pedersen 用他们的[对冲 beta（BAB）和垃圾质量（QMJ）因子](http://www.econ.yale.edu/~af227/)扩大了我们的世界。Fama/French 和 Frazzini/Pedersen 的综合因子集为我们提供了对美国及全球股市历史表现的重要见解。

幸运的是，作者还提供了他们的因子。~不幸的是，BAB 和 QMJ 并没有像 Fama/French SMB 和 HML 那样更新。~（实际上发现这不再正确[Frazzini 数据库](http://www.econ.yale.edu/~af227/data_library.htm)）。尽管如此，将这些因子与 R 包 factorAnalytics 和 rCharts 结合使用，使我们能够做一些令人惊叹的事情。下面是一个快速示例。更多内容即将推出。

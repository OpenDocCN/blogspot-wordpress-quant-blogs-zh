<!--yml

分类: 未分类

日期：2024-05-18 14:03:15

-->

# 时间机器测试（第一部分）- 量子金融家

> 来源：[`quantumfinancier.wordpress.com/2010/05/10/time-machine-test-part-1/#0001-01-01`](https://quantumfinancier.wordpress.com/2010/05/10/time-machine-test-part-1/#0001-01-01)

这一系列的帖子是基于[CSS Analytics 的“时间机器”系列帖子](http://cssanalytics.wordpress.com/2009/09/14/busting-the-efficient-markets-hypothesis-the-adaptive-market-time-machine/)。我建议你阅读它，因为这不是我的原创想法。但是，我认为我的实现与 CSS Analytics 稍有不同。

下面的结果代表我对不同股票指数使用我的算法进行的回测，该算法使用了每个股票的所有免费历史数据。我使用了指数数据，因为可用的数据点远在历史之前。我确实测试了可用的 ETF，结果相似。下面呈现的所有结果都是无摩擦的。

标准普尔 500 指数

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/time-machine-test-gspc2.jpg)

罗素 2000 指数

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/time-machine-test-rut.jpg)

纳斯达克 100 指数

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/time-machine-test-ndx.jpg)

S&P/TSX 综合指数（加拿大）

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/time-machine-test-gsptse.jpg)

富时 100（英国）

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/time-machine-test-ftse.jpg)

日经 225 指数（日本）

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/time-machine-test-n225.jpg)

恒生指数（中国）

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/time-machine-test-hsi.jpg)

摘要

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/time-machine-test-results.jpg)

如上所示，算法非常稳健，并且对不同的市场环境以及所有这些指数的市场行为差异都适应得相当好。尽管如此，我认为这是一个非常好的且简单的概念，仍然可以改进。

在接下来的几篇帖子中，我会尝试对算法进行一些修改。目前，你可以期待看到不同资产类别的测试：商品、期货、货币等。我还想尝试用非参数的 Wilcoxon 符号秩检验替换 t 检验，看看当我们摒弃了在显著性检验中假设正态分布时，策略的表现如何。我还有其他一些想法来改进算法，敬请期待！

量化金融（QF）

<!--yml

类别：未分类

日期：2024-05-18 14:03:23

-->

# (第二部分) 时间机器测试 – 非参数统计过滤器 – 量子金融家

> 来源：[`quantumfinancier.wordpress.com/2010/05/11/part-2-time-machine-test-%e2%80%93-non-parametric-statistical-filter/#0001-01-01`](https://quantumfinancier.wordpress.com/2010/05/11/part-2-time-machine-test-%e2%80%93-non-parametric-statistical-filter/#0001-01-01)

如昨日所承诺，我对 CSS Analytics 最初提出的“时间机器”策略进行了微调。若你尚未阅读，请务必查阅这些关于统计过滤器及其在交易系统中重要性的背景文章：

– [自适应时间机器：统计过滤器的重要性](http://cssanalytics.wordpress.com/2009/09/16/the-adaptive-time-machine-the-importance-of-statistical-filters/) – CSS Analytics

– [交易型与基于信心的交易策略](http://marketsci.wordpress.com/2009/04/01/transactional-vs-confidence-based-trading-strategies/) – MarketSci

在昨天的帖子中，我采用了学生 t 检验方法来过滤算法可选择的 50 种策略的重要性。你可能知道，学生 t 分布用于估计*正态分布总体*的均值。这种对分布的假设与市场抛给我们的肥尾回报相矛盾。为了放宽正态性假设，可以使用非参数统计检验。非参数统计对基础分布的假设较少，因此可能更稳健，这使得它成为“时间机器”算法的理想选择。更多关于 Wilcoxon 符号秩检验的阅读，请访问：[`en.wikipedia.org/wiki/Wilcoxon_signed-rank_test`](http://en.wikipedia.org/wiki/Wilcoxon_signed-rank_test)。

对于此次测试，我采用了 Wilcoxon 符号秩检验而非学生 t 检验来确定策略的重要性。以下结果是针对使用 95%显著性过滤器的 S&P 500 策略。

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/time-machine-test-wilcox-gspc.png)

![](https://quantumfinancier.wordpress.com/wp-content/uploads/2010/05/time-machine-test-wilcox-results.png)

所得结果与之前相比并无太大差异。有趣的是，使用 Wilcoxon 检验时最大回撤更小，这可能归因于统计检验的增强稳健性。目前我将继续在不同的股票指数和资产类别上测试该算法，敬请关注。

QF

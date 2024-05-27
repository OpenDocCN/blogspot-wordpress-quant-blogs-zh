<!--yml

分类：未分类

日期：2024-05-12 18:55:24

-->

# 量化交易：外汇订单流作为预测器

> 来源：[`epchan.blogspot.com/2018/02/fx-order-flow-as-predictor.html#0001-01-01`](http://epchan.blogspot.com/2018/02/fx-order-flow-as-predictor.html#0001-01-01)

订单流是带符号的交易大小，并且早已被认为可以预测未来的价格变动。（参见

[Lyons，2001](http://amzn.to/2DKKn8j)

，或者

[Chan，2017](https://www.amazon.com/Machine-Trading-Deploying-Computer-Algorithms/dp/1119219604/ref=as_sl_pc_tf_til?tag=quantitativet-20&linkCode=w00&linkId=b6c22e03b04fdcf3f6a14bc4b5891edb&creativeASIN=1119219604)

。) 然而，获取此类数据通常相当困难或昂贵，无论是历史数据还是实时数据。这在外汇交易中尤为正确，这些交易是在场外发生的。认识到这种数据的利润潜力，大多数外汇市场运营商将它们视为他们的瑰宝，永远不会透露给客户。但是最近 FXCM，一个外汇经纪商，已经慷慨地提供了他们的

[专有数据](https://www.fxcm.com/uk/trading-services/market-data/)

，并且我利用了这个数据来测试一个简单的外汇交易策略，该策略使用 EURUSD 的订单流。

首先，让我们检查一下数据的一些一般特征。这些数据捕获了 2017 年 FXCM 上发生的所有外汇交易，时间戳以毫秒为单位，还包括交易价格和带符号的交易大小。如果交易是由买入市价订单产生的，则其符号为正；如果是由卖出产生的，则符号为负。如果我们取这些交易大小的绝对值，并按每小时间隔将它们相加，我们可以得到通常的每小时成交量（点击放大）汇总了 1 年数据集：

难怪 16:00-17:00 的成交量最高，因为 16:00 是基准利率（“

[fix](https://www.investopedia.com/articles/forex/031714/how-forex-fix-may-be-rigged.asp)

的确定。当然，9:00-10:00 的次高峰是伦敦商业日的开始。

接下来，我计算了 EURUSD 的每日总订单流（纽约午夜结束），并建立了过去 20 天每日订单流的直方图。然后我确定了每个订单流五分位数的平均次日回报率。（也就是说，我根据前一天的订单流落在哪个五分位数中，将次日回报率分到每个箱子中，然后取每个箱子中的回报率平均值。）结果令人满意：

![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEh0lYe72txg8HeMMDjAT2uOxBZ0P10mW95oTNsPsOPDVzlc7bhvfjpr4VyYwozZ-UgnhkcWJJG538nLQYhFhGcI9pxaocM9gXhMNkIcRj9-VQKMwPEjp34MoSv7lPuGcEqxVVSGOw/s1600/order+flow+return+quintiles.png)

我们可以看到，次日的平均回报几乎随着前一天的订单流而单调增加。前五分之一和后五分之一的差距约为 12 bps，这相当于约 30%的年化回报。这并不意味着我们将产生 30%的年化回报，因为我们将无法在今天的回报（如果订单流在前五分之一或后五分之一）与前一天回报（其订单流在相反的极端）之间进行套利。尽管如此，这还是令人鼓舞的。此外，这也说明，即使订单流必须基于逐笔基础计算（我不是这种方法的粉丝），但结果仍然如此。

[大宗体积分类](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=2182819)

技术），它可以用在低频交易策略中。

（有人可能会诱惑我们也对未来回报进行回归，以过去订单流为自变量，但结果在统计学上不显著。显然，只有订单流的前五分之一和后五分之一才是有预测性的。这种情况实际上相当

[常见](https://www.bloomberg.com/news/articles/2017-06-27/ex-bridgewater-quant-says-smart-beta-etfs-use-factors-all-wrong)

在金融领域，这就是为什么线性回归在交易策略中没有被更广泛应用的原因。)

最后，在回测之前再进行一次理智的检查。我想看看买入交易（由买入市价订单产生的交易）是否以高于 bid 价格成交，而卖出交易是否以低于 ask 价格成交。以下是纽约时间（时间为一天中的某个时刻）的一天的图表：

我们可以看到，总的来说，交易和报价价格之间的关系是满足的。我们实际上不能期望这种关系保持 100%，因为报价在交易发生后微秒内移动，并且变化被报告为与交易同步，或者当交易或报价变化报告有延迟时。

现在我们准备构建一个简单的交易策略，该策略使用订单流作为预测因子。我们可以在每日结束时简单地购买 EURUSD，当时日的流量在最后 20 天的值中的前五分之一，并持有 1 天，当它处于最低五分之一时，我们就做空。由于我们的日流量是在纽约时间午夜测量的，所以我们也将日的结束时间定义为那时。如果我们使用伦敦或苏黎世的午夜时间，也会得到类似的结果，这表明我们可以错开我们的仓位。在我的回测中，我已经减去了 0.20 bps 的佣金（基于 Interactive Brokers），并且我假定我用市价订单在 ask 价格买入，在 bid 价格卖出。以下是权益曲线：

年复合增长率（CAGR）为 13.7%，夏普比率为 1.6。对于一个单一因子模型来说，这还不错！

*致谢*

:  我感谢

[Zachary David](http://zacharydavid.com/)

感谢他对这篇稿件的审阅和评论，当然还有 FXCM 提供的

[数据](https://www.fxcm.com/uk/trading-services/market-data/)

为这项研究。

===

行业更新

1)

[Qcaid](http://www.qbitia.com/)

是一个基于云的平台，为交易者提供回测、执行和模拟设施。他们还提供服务器和数据源。

2)

[Cadre 如何使用机器学习针对房地产市场](https://blog.cadre.com/how-cadre-uses-machine-learning-to-target-real-estate-markets-3c03ca1dac26)

。

3) 看看 Quantopian 的新

[教程](https://www.quantopian.com/tutorials/getting-started)

关于进入量化金融的入门课程。

4) 一个新的基于 Matlab 的回测和实时交易平台可供下载

[这里](https://github.com/EliteQuant/EliteQuant_Matlab)

。

5) 一个关于开源算法交易工具的好资源页面在

[QuantNews](http://www.quantnews.com/resources/)

。

**我的即将进行的研讨会**

2 月 24 日和 3 月 3 日：

[算法期权策略](http://www.epchan.com/workshops)

这个在线课程专注于日内回测和投资组合期权策略。不会讨论让人烦恼的期权定价理论，因为重点是套利交易。

June 4-8: 伦敦研讨会

这些紧张的 8-16 小时的研讨会涵盖了

[算法期权策略](http://www.globalmarkets-training.co.uk/algorithmicoptions.html)

，

[量化动量策略](http://www.globalmarkets-training.co.uk/quantmomentum.html)

，并且

[日内交易与市场微观结构](http://www.globalmarkets-training.co.uk/intradaytrading.html)

。典型的课程规模不超过 10 人。他们可能有资格获得 CFA 协会的持续教育学分。（额外福利：环境很不错

[查看](https://twitter.com/chanep/status/908250965786144769)

泰晤士河，还有大量的免费食物。）

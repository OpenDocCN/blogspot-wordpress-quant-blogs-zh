<!--yml

分类：未分类

日期：2024-05-18 05:31:17

-->

# Kappa 架构：贝叶斯在线学习模型 | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2016/06/08/kappa-architecture-bayesian-online-%c2%adlearning-model/#0001-01-01`](https://mdavey.wordpress.com/2016/06/08/kappa-architecture-bayesian-online-%c2%adlearning-model/#0001-01-01)

## Kappa 架构：贝叶斯在线学习模型

来自 Strata + Hadoop World London 2016 的“在电信行业中应用 Kappa [架构](https://www.oreilly.com/ideas/applying-the-kappa-architecture-in-the-telco-industry)”提供了一个很好的阅读材料。许多公司实际上并没有数据量问题，但他们确实有“更短的时间限制和不断提高的准确性需求”，希望通过使用 AI 来实现业务转型。

这篇文章中最突出的第一句话是：

> 贝叶斯在线学习模型用于检测新颖性

对于公司来说，有许多用例可以利用新颖性检测客户和员工数据集。

Kappa 架构对我之前博客中提到的 lambda 架构是一个很好的补充。流式处理是当今的唯一途径，尤其是在 Apache Spark Streaming 的发展过程中——“批处理是流处理的一个子集。”

不可变数据源和原始数据与之前一段时间在其他地方博客中提到的 ELT（提取、加载、转换）观点很好地相关联

不幸的是，这篇文章没有提到用于贝叶斯异常检测的机器学习库是哪一个😦

有趣的是，这里使用了 Apache [Flink](https://flink.apache.org/)而不是 Apache [Spark](http://spark.apache.org/)。看到 Apache [Kafka](http://kafka.apache.org/)作为数据通道真是太好了😊

~ mdavey 于 2016 年 6 月 8 日。

发表于[数据](https://mdavey.wordpress.com/category/data/)

Tags: [Kappa](https://mdavey.wordpress.com/tag/kappa/), [MachineLearning](https://mdavey.wordpress.com/tag/machinelearning/)

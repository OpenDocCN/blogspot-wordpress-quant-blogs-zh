<!--yml

分类：未分类

日期：2024-05-18 05:35:02

-->

# 机器学习与本体论 | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2016/03/23/machine-learning-and-ontologies/#0001-01-01`](https://mdavey.wordpress.com/2016/03/23/machine-learning-and-ontologies/#0001-01-01)

## 机器学习与本体论

在考虑基于本体的数据源对[H2O](http://www.h2o.ai/)和机器学习世界的摄取时，我发现了两篇有趣的论文：

+   本体[匹配](http://homes.cs.washington.edu/~pedrod/papers/hois.pdf)：一种机器学习方法

+   使用机器学习支持[持续](http://wortschatz.uni-leipzig.de/~fwitschel/papers/ekaw10.pdf)本体开发

我不确定这些是否帮助了我思考的过程，但它们仍然很有趣。在许多方面，我在想本体是否有助于模型/算法的使用，或者我最终会陷入数据过载:)

顺便看看“高盛如何使用知识创建信息[优势](http://conferences.oreilly.com/strata/stratany2014/public/schedule/detail/37837)“的幻灯片。尽管幻灯片不是充满细节，但第 5 张幻灯片至少提供了一个高层次的架构，并详细介绍了本体使用的信息。看起来同样的报告去年[又](http://conferences.oreilly.com/strata/big-data-conference-uk-2015/public/schedule/detail/39810)发表了一次——不幸的是，这次没有幻灯片可供使用。

> 在高盛的方法中，权威的原始数据源存储在 Hadoop 的企业数据湖中，存储在 HDFS 中。为了表示我们的知识领域，高盛公司开发了一个企业本体，表示其业务概念。上层本体以 OWL 格式表示，并描述类结构和数据转换规则。这些规则随后在自开发的 Hadoop 过程中被利用，将数据转换为 RDF 格式的语义一致的信息。利用底层本体中的断言和高级概念生成转换数据上的规则集，创建由数十亿个节点和边组成的“大数据图”。

~ mdavey 于 2016 年 3 月 23 日

发布在[未分类](https://mdavey.wordpress.com/category/uncategorized/)

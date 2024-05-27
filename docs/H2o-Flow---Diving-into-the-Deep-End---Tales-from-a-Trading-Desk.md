<!--yml

类别：未分类

日期：2024 年 05 月 18 日 05 时 35 分 24 秒

-->

# H2o Flow – Diving into the Deep End | Tales from a Trading Desk

> 来源：[`mdavey.wordpress.com/2016/03/16/h2o-flow-diving-into-the-deep-end/#0001-01-01`](https://mdavey.wordpress.com/2016/03/16/h2o-flow-diving-into-the-deep-end/#0001-01-01)

[H2o](http://www.h2o.ai/resources/)和[Flow](https://github.com/h2oai/h2o-3/blob/master/h2o-docs/src/product/flow/README.md)安装简单，只需要运行以下命令即可启动 H2o，然后通过 localhost:54321 获得对 Flow 的访问：

> java -jar build/h2o.jar

安装时有许多可用的示例，比如：

+   百万首歌二进制分类演示

+   GLM 教程

+   KDDCup 2009 流失预测演示

+   预测航班延误

在 H2o 的公共测试[S3](http://s3.amazonaws.com/h2o-public-test-data)上有大量的测试数据可用。

如果您已经通过各种演示和[tutorials](http://blog.h2o.ai/2014/11/introducing-flow/)，现在是时候开始处理一些您自己的数据了。我已经（或者没有）选择了创建一些样本数据测试，将其保存在.CSV 文件中，然后使用 Help/Assist Me/importFiles 功能将其加载到 Flow 中。加载了多个样本数据.CSV 文件后，我可以执行 Help/Assist Me/getFrames 来查看加载的数据文件，以及每一个 Frame。

接下来，模型。有多种算法可供选择：

> 当感兴趣的变量涉及对速率、事件或连续测量的预测或推理，或者涉及一组环境条件如何影响因变量的问题时，请使用 GLM。以下是一些例子：“什么属性决定哪些客户会购买，哪些不会？”，“在给定一组特定的制造条件下，将会有多少个单位出现故障？”，“在给定的时间范围内，有多少客户会联系帮助支持？”
> 
> 随机森林（RF）是一个强大的分类工具。在给定一组数据时，RF 生成一系列分类树，而不是单个分类树。每棵树都为给定一组属性生成一个分类。H2O 树的每个分类可以被看作是一次投票；得票最多的决定分类。
> 
> 当数据是一组在人群中可能不同的属性时，且目标是分类时，使用 K-Means。以下是一些例子：竞争对手在关键维度上有什么不同？ 一个特定的市场是如何分割的？ 哪些维度对于区分目标人群的成员最重要？

一旦您决定了模型的算法（可能是基于大量阅读和学习，如果您不是一个熟练的数据科学家），接下来您需要用可用的 n [options](http://h2o-release.s3.amazonaws.com/h2o-dev/rel-shannon/2/docs-website/h2o-docs/index.html#%E2%80%A6%20Building%20Models)配置您的模型。

Flow 似乎只提供了将数据文件导入到数据框架的功能，以及将数据框架拆分为 2 个或更多个数据框架的功能。由于模型似乎只能接受一个训练数据框架和一个验证数据框架，我没有找到一种可以像“使用 Sparkling Water 和 Apache Spark 构建机器学习应用”的[代码](http://blog.cloudera.com/blog/2015/10/how-to-build-a-machine-learning-app-using-sparkling-water-and-apache-spark/)中所示的使用 Spark 进行表格合并，然后将 Spark RDD 发布为 H2O 数据框架的方法。所以，当在 Flow land 中操作时，确保只从文件中加载了一个数据框架是很重要的，或者可能我错过了 Flow 中的某个功能？

现在，我进入了模型选项的领域。我也打算回去再试试 R-Studio 和 H2O。

“‘Ask Craig’- 使用 Sparkling Water 确定 Craigslist 的职位类别”提供了一篇分为 2 部分的[文章](http://blog.h2o.ai/2015/06/ask-craig-sparkling-water/)，是值得一读的。

～ 由 mdavey 于 2016 年 3 月 16 日发布。

发表于[数据](https://mdavey.wordpress.com/category/data/)

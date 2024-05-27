<!--yml

分类：未分类

日期：2024-05-18 05:35:37

-->

# 数据科学算法之旅 | 一个交易台的故事

> 来源：[`mdavey.wordpress.com/2016/03/14/data-science-algorithms-journey/#0001-01-01`](https://mdavey.wordpress.com/2016/03/14/data-science-algorithms-journey/#0001-01-01)

## 数据科学算法之旅

当你与[H2O](http://www.h2o.ai/)或类似工具一起踏上这条路时，一旦你完成了软件的安装，下一个问题很可能是，我应该从哪里开始，以及我应该在这些数据上使用什么[算法](https://msdn.microsoft.com/en-us/library/ms175595.aspx)。

安装 H2O 非常容易——我选择了在[GitHub](https://github.com/h2oai/h2o-3)上的内容：

> git clone [`github.com/h2oai/h2o-3.git`](https://github.com/h2oai/h2o-3.git)

接下来是配方 1——但是 docs:runGenerateRESTAPIDocs 步骤失败了 😦 运行起来就像这样简单：

> java -jar build/h2o.jar

这就带我们到了[Flow](http://blog.h2o.ai/2014/11/introducing-flow/)，通过：

> [`localhost:54321/`](http://localhost:54321/)

最后带我们到算法和数据。H2O 提供了[以下](http://www.h2o.ai/product/algorithms/)数据准备、机器[学习](http://docs.h2o.ai/h2oclassic/resources/algoroadmap.html)和模型置信度的高层次概述。

数据和洞察力是相辅相成的。在许多情况下，一旦你拥有了相同的数据，你会进一步确定你想要的额外数据，以帮助你进一步洞察。这篇关于[公共安全](http://blog.h2o.ai/2015/04/deep-learning-public-safety/)的文章提供了许多关于解决问题的想法。例如，你可以想象对随时间变化的销售活动感兴趣，与股市的涨跌相结合，也许还有销售周期的持续时间，以及它是如何受股市影响的。

广义低秩[模型](http://www.h2o.ai/verticals/algos/glrm/)看起来特别有趣，尤其是这个[视频](https://youtu.be/gEZtZRANeLc)。

如果你有销售数据，那么按照类似的路径进行客户[智能](http://www.h2o.ai/use-cases/customer-intelligence/)用例可能是一个有趣的起点。对于用例来说，没有提供样本数据集是一件遗憾的事情。

~ 由 mdavey 于 2016 年 3 月 14 日发布。

Posted in [Data](https://mdavey.wordpress.com/category/data/)

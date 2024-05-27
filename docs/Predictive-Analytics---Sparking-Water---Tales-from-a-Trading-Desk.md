<!--yml

分类：未分类

日期：2024-05-18 05:37:14

-->

# 预测分析——Sparking Water | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2015/12/08/predictive-analytics-sparking-water/#0001-01-01`](https://mdavey.wordpress.com/2015/12/08/predictive-analytics-sparking-water/#0001-01-01)

## 预测分析——Sparking Water

如果你还没有查看[H2O](http://h2o.ai/product/)，那么花点时间研究[软件](http://www.kdnuggets.com/2015/01/interview-arno-candel-h20-deep-learning.html)是个不错的选择。除了可以用[R](http://www.r-bloggers.com/things-to-try-after-user-part-1-deep-learning-with-h2o/)做的酷炫的事情外，还有[Spark](https://databricks.com/blog/2014/06/30/sparkling-water-h20-spark.html)和[Sparking Water](http://blog.cloudera.com/blog/2015/10/how-to-build-a-machine-learning-app-using-sparkling-water-and-apache-spark/)——很酷的项目名称。有人用 Sparking Water 处理交易数据吗？

CitiBike New York 演示和代码可在[此处](http://h2o.ai/blog/2015/02/strata-2015/)找到。

[ML](http://blog.cloudera.com/blog/2015/10/how-to-build-a-machine-learning-app-using-sparkling-water-and-apache-spark/) [库](https://spark.apache.org/docs/latest/mllib-guide.html)的算法提供了从多个角度使用 H2O 的机会：

+   动态时间规整——客户阅读的内容（例如交易想法、研究）是否影响了交易行为？客户的定期模式

+   （隐藏）马尔可夫模型——预测客户接下来可能进行的交易

+   使用 ALS 的协同过滤——类似于[Netflix](https://en.wikipedia.org/wiki/Netflix_Prize)，推荐交易、研究、交易想法。

+   Logitistic 回归——找出二元响应变量（例如客户是否击中价格）之间的关系。

~ mdavey 于 2015 年 12 月 8 日。

发布在[数据](https://mdavey.wordpress.com/category/data/)分类下

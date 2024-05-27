<!--yml

类别：未分类

date: 2024-05-18 05:47:35

-->

# 使用交替最小二乘法（ALS）进行交易研究/建议 | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2014/08/07/trading-researchidea-recommendation-using-alternating-least-squares-als/#0001-01-01`](https://mdavey.wordpress.com/2014/08/07/trading-researchidea-recommendation-using-alternating-least-squares-als/#0001-01-01)

## 使用交替最小二乘法（ALS）进行交易研究/建议

[Spark](http://spark.apache.org/docs/latest/streaming-programming-guide.html) 引起了很多人关注。在单一银行平台空间使用 Spark 的明显想法是帮助卖方客户识别交易建议/研究/评论，以协助他们管理投资组合。作为一个起点，阅读 Spark[电影](http://mlnick.github.io/blog/2013/04/01/movie-recommendations-and-more-with-spark/)建议和[MLlib](http://spark.apache.org/docs/latest/mllib-collaborative-filtering.html)文章在 ampcamp 上，提供了协同过滤和交替最小二乘法（ALS）的详细信息。还提供了代码 🙂

[MLlib](http://spark.apache.org/docs/latest/mllib-guide.html) 是 Spark 对一些常见机器学习[算法](http://www.slideshare.net/MrChrisJohnson/collaborative-filtering-with-spark)和工具的实现，包括分类、回归、聚类、协同过滤、维度降低以及底层优化原语。

也许还会阅读 ampcamp 的 Spark Streaming[文章](http://ampcamp.berkeley.edu/3/exercises/realtime-processing-with-spark-streaming.html)。

最后，看看 Andrew Psaltis 的视频，探索点击流分析的实时 Map Reduce：[`berlinbuzzwords.de/session/real-time-map-reduce-exploring-clickstream-analytics-spark-streaming-kafka-and-websockets`](http://berlinbuzzwords.de/session/real-time-map-reduce-exploring-clickstream-analytics-spark-streaming-kafka-and-websockets)

有了上述所有内容，开始使用 Spark Streaming 向客户提供推荐阅读材料的警报相对容易。

为了深入理解发生了什么，试试这篇[文章](http://labs.yahoo.com/files/HuKorenVolinsky-ICDM08.pdf)。要留意“冷启动”问题：

> 无法处理系统中的新产品，内容基础方法将足够。

更进一步，用户数据和交易内容结合交易活动、报价活动以及可能的客户关系管理（CRM）数据将增强建议。

最后，了解一下你是否能从传播的角度利用协同过滤[算法](https://spark.apache.org/docs/latest/mllib-collaborative-filtering.html)，来可能地推荐一种关于交易价格的传播，会很有趣。 logistics [回归](https://spark.apache.org/docs/latest/mllib-linear-methods.html#logistic-regression)或许对于根据 RFQ 接受/拒绝数据的价格敏感性来优化客户传播更为有趣。

~ mdavey 于 2014 年 8 月 7 日。

发布在[数据](https://mdavey.wordpress.com/category/data/)分类中。

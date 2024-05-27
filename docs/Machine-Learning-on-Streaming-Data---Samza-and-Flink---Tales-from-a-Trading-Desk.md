<!--yml

category: 未分类

date: 2024-05-18 05:33:07

-->

# Machine Learning on Streaming Data – Samza and Flink | Tales from a Trading Desk

> 来源：[`mdavey.wordpress.com/2016/04/28/machine-learning-on-streaming-data-samza-and-flink/#0001-01-01`](https://mdavey.wordpress.com/2016/04/28/machine-learning-on-streaming-data-samza-and-flink/#0001-01-01)

## Machine Learning on Streaming Data – Samza and Flink

根据一些评论，再加上各种网上阅读，我得出的印象是 Spark 和 Storm 不是在流数据机器学习平台上的最新解决方案——也许我错了？Apache [Samza](http://samza.apache.org/)和[Flink](http://flink.apache.org/)似乎是崭露头角的新秀。有一些各种流处理引擎的比较——其中一个[在这里](http://www.altaterra.net/blogpost/288668/225612/Which-Stream-Processing-Engine-Storm-Spark-Samza-or-Flink)，另一个[在这里](http://www.cakesolutions.net/teamblogs/comparison-of-apache-stream-processing-frameworks-part-1)。

Samza 非常有意思，因为它使用了我非常喜欢的一种技术，Apache Kafka 🙂 Flink 然而似乎是最新露头的新秀:-)，根据这个简单的代码[比较](http://www.cakesolutions.net/teamblogs/comparison-of-apache-stream-processing-frameworks-part-1)，它提供了一个干净的 API。

dataArtisans “Kafka + Flink: A [practical](http://data-artisans.com/kafka-flink-a-practical-how-to/), how-to guide”文章提供了一些关于如何连接 Kafka 和 Flink 的方向，这在很多方面可能是运行流数据上机器学习模型的方法。

最后，虽然有些旧了，“Apache Flink: API, runtime, and project [roadmap](http://www.slideshare.net/KostasTzoumas/apache-flink-api-runtime-and-project-roadmap)”幻灯片 62 提供了 Flink 与机器学习库集成的路线图视图——幻灯片 67 也提到了 H2O，在幻灯片 71 上有提及。

The next bus: Apache [Kudu](http://getkudu.io/)?

~ by mdavey on April 28, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/)

Tags: [MachineLearning](https://mdavey.wordpress.com/tag/machinelearning/), [StreamingData](https://mdavey.wordpress.com/tag/streamingdata/)

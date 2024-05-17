<!--yml
category: 未分类
date: 2024-05-18 05:47:35
-->

# Trading Research/Idea Recommendation using Alternating Least Squares (ALS) | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2014/08/07/trading-researchidea-recommendation-using-alternating-least-squares-als/#0001-01-01](https://mdavey.wordpress.com/2014/08/07/trading-researchidea-recommendation-using-alternating-least-squares-als/#0001-01-01)

## Trading Research/Idea Recommendation using Alternating Least Squares (ALS)

[Spark](http://spark.apache.org/docs/latest/streaming-programming-guide.html) is generating a lot of interest.  Obvious ideas for using Spark in the Single Bank Platform space is around helping the sell-sides clients in identify trade ideas/research/commentary to assist them in their portfolio.  As a starting point, its worth reading the Spark [movie](http://mlnick.github.io/blog/2013/04/01/movie-recommendations-and-more-with-spark/) recommendation with [MLib](http://spark.apache.org/docs/latest/mllib-collaborative-filtering.html) [article](http://ampcamp.berkeley.edu/big-data-mini-course/movie-recommendation-with-mllib.html) over on ampcamp, which provides details on collaborative filtering and alternating least squares (ALS).  Code is also provided 🙂

[MLlib](http://spark.apache.org/docs/latest/mllib-guide.html) is a Spark implementation of some common machine learning [algorithms](http://www.slideshare.net/MrChrisJohnson/collaborative-filtering-with-spark) and utilities, including classification, regression, clustering, collaborative filtering, dimensionality reduction, as well as underlying optimization primitives

Its probably also having a read of the ampcamp’s Spark Streaming [article](http://ampcamp.berkeley.edu/3/exercises/realtime-processing-with-spark-streaming.html).

Finally, check out Andrew Psaltis’s video, Real-time Map Reduce: Exploring Clickstream [Analytics](http://berlinbuzzwords.de/session/real-time-map-reduce-exploring-clickstream-analytics-spark-streaming-kafka-and-websockets) with Spark Streaming, Kafka and WebSockets

With all the above, its relatively easy to begin to look at using Spark Streaming to deliver alerts to client on recommended reading material.

For a deep understanding of what is going on, try this [article](http://labs.yahoo.com/files/HuKorenVolinsky-ICDM08.pdf).  Be mindful of the ‘cold start’ issue:

> inability to address products new to the system, for which content based approaches would be adequate.

Taking this a step further, user data and trade content with trading activity, quoting activity and possible CRM data would enhance the recommendations.

Finally, it would be interesting to know if you could take advantage of Collaborative [Filtering](https://spark.apache.org/docs/latest/mllib-collaborative-filtering.html) from a spreading perspective, to possible recommend a spread on the trade price for an instrument.  Logistic [Regression](https://spark.apache.org/docs/latest/mllib-linear-methods.html#logistic-regression) maybe more interesting for optimize the client spread based on the price sensitivity from RFQ accept/reject data.

~ by mdavey on August 7, 2014.

Posted in [Data](https://mdavey.wordpress.com/category/data/)
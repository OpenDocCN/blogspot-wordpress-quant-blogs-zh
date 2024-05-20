<!--yml
category: 未分类
date: 2024-05-18 05:37:14
-->

# Predictive Analytics – Sparking Water | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2015/12/08/predictive-analytics-sparking-water/#0001-01-01](https://mdavey.wordpress.com/2015/12/08/predictive-analytics-sparking-water/#0001-01-01)

## Predictive Analytics – Sparking Water

If you haven’t looked at [H2O](http://h2o.ai/product/) yet, its probably working spending a bit of time with the [software](http://www.kdnuggets.com/2015/01/interview-arno-candel-h20-deep-learning.html).  Apart from the cool stuff you can do with [R](http://www.r-bloggers.com/things-to-try-after-user-part-1-deep-learning-with-h2o/), there is [Spark](https://databricks.com/blog/2014/06/30/sparkling-water-h20-spark.html), and [Sparking Water](http://blog.cloudera.com/blog/2015/10/how-to-build-a-machine-learning-app-using-sparkling-water-and-apache-spark/) – cool project name.  Anyone using Sparking Water with trade data?

CitiBike New York demo and code is available [here](http://h2o.ai/blog/2015/02/strata-2015/).

The [ML](http://blog.cloudera.com/blog/2015/10/how-to-build-a-machine-learning-app-using-sparkling-water-and-apache-spark/) [library](https://spark.apache.org/docs/latest/mllib-guide.html) of algorithms offer the opportunity to use H2O from a number of angles:

*   Dynamic Time Warping – does what the client read (e.g. trade ideas, research) impact the trading behaviour? recurring client patterns
*   (Hidden) Markov Models – predicting what trade a client might do next
*   Collaborative Filtering with ALS – Similar to [Netflix](https://en.wikipedia.org/wiki/Netflix_Prize), recommend trades, research, trading ideas.
*   Logitistic Regression – find the relationship between a binary response variable e.g. if the client hit a price.

~ by mdavey on December 8, 2015.

Posted in [Data](https://mdavey.wordpress.com/category/data/)
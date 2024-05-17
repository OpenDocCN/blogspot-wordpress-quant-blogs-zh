<!--yml
category: 未分类
date: 2024-05-18 05:35:37
-->

# Data Science Algorithms Journey | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/03/14/data-science-algorithms-journey/#0001-01-01](https://mdavey.wordpress.com/2016/03/14/data-science-algorithms-journey/#0001-01-01)

## Data Science Algorithms Journey

As you venture down the road with [H2O](http://www.h2o.ai/) or similar tools, once you’ve got passed installing the software, the next problem is more than likely going to get, what data should I start with, and what [algorithms](https://msdn.microsoft.com/en-us/library/ms175595.aspx) shall I use on the data.

H2O is very easy to install – I went with what was on [GitHub](https://github.com/h2oai/h2o-3):

> git clone [https://github.com/h2oai/h2o-3.git](https://github.com/h2oai/h2o-3.git)

Followed by Recipe 1 – however the docs:runGenerateRESTAPIDocs step failed 😦  Running is as easy as:

> java -jar build/h2o.jar

Which then brings us to [Flow](http://blog.h2o.ai/2014/11/introducing-flow/) via:

> [http://localhost:54321/](http://localhost:54321/)

Which finally brings us to algorithms, and data.  H2O offers the [following](http://www.h2o.ai/product/algorithms/) high level overview of data preparation, machine [learning](http://docs.h2o.ai/h2oclassic/resources/algoroadmap.html) and model confidence.

Data and insight go hand in hand.  In many ways, once you have same data, you’ll then identify the additional data you want to aid you on further insight.  This posting on [Public Safety](http://blog.h2o.ai/2015/04/deep-learning-public-safety/) offers a number of thought around tacking problem.  For example, you can imagine being interested in looking at sales activity over time, married to the highs and lows of the stock market, and maybe also the duration of the sales cycle, and how its influenced buy the stock market.

Generalized Low Rank [Models](http://www.h2o.ai/verticals/algos/glrm/) looks particularly interesting, especially this [video](https://youtu.be/gEZtZRANeLc).

If you have sales data, then following a similar path to the Customer [Intelligence](http://www.h2o.ai/use-cases/customer-intelligence/) use case is probably an interesting starting point.  Its a shame a sample data set isn’t provide for the use cases.

~ by mdavey on March 14, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/)
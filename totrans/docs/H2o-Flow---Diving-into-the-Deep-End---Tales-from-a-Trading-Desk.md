<!--yml
category: 未分类
date: 2024-05-18 05:35:24
-->

# H2o Flow – Diving into the Deep End | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/03/16/h2o-flow-diving-into-the-deep-end/#0001-01-01](https://mdavey.wordpress.com/2016/03/16/h2o-flow-diving-into-the-deep-end/#0001-01-01)

[H2o](http://www.h2o.ai/resources/) and [Flow](https://github.com/h2oai/h2o-3/blob/master/h2o-docs/src/product/flow/README.md) are simple to [install](https://github.com/h2oai/h2o-3).  Once installed, just run the following command to start H2o, and thus get access to Flow via localhost:54321:

> java -jar build/h2o.jar

There are numerous samples available with the install, such as:

*   Million Song Binary Classification Demo
*   GLM Tutorial
*   KDDCup 2009 Churn Prediction Demo
*   Predicting Airline Delays

There is a lot of test data available on H2o’s public tests [S3](http://s3.amazonaws.com/h2o-public-test-data).

If you’ve made it though various demos and [tutorials](http://blog.h2o.ai/2014/11/introducing-flow/), its now time to crunch some of your own data.  Correctly (or not), I’ve gone down the road of creating some sample data tests in .CSV files which I then load into Flow using the Help/Assist Me/importFiles function.  With a number of samples data .CSV files loaded, I can execute Help/Assist Me/getFrames to see the data files loaded, and a Frame for each.

Next up, the Model.  There are a number of algorithm to select for your model:

> Use GLM when the variable of interest relates to predictions or inferences about a rate, an event, or a continuous measurement or for questions about how a set of environmental conditions influence the dependent variable.Here are some examples:“What attributes determine which customers will purchase, and which will not?”,“Given a set of specific manufacturing conditions, how many units produced will fail?”,“How many customers will contact help support in a given time frame?”
> 
> Random Forest (RF) is a powerful classification tool. When given a set of data, RF generates a forest of classification trees, rather than a single classification tree. Each of these trees generates a classification for a given set of attributes. The classification from each H2O tree can be thought of as a vote; the most votes determines the classification.
> 
> Use K-Means when data are a set of attributes on which the members of the population likely differ and the objective is classification. Here are some examples: How do competitors differ from one another on critical dimensions?  How is a particular market segmented?  Which dimensions are most important to differentiating between members of a population of interest?

Once you’ve decide on the algorithm to use for your model (possibly based on a lot of reading and learning if your not a skilled data scientist), you then need to configure your model with the n [options](http://h2o-release.s3.amazonaws.com/h2o-dev/rel-shannon/2/docs-website/h2o-docs/index.html#%E2%80%A6%20Building%20Models) available.

Flow appears to only offer the import of a data file into a Frame, and the splitting of a Frame into 2 or more Frames.  Given a Model appears to only take a training and validation frame, I don’t see a way to combine Frame similar to the [code](http://blog.cloudera.com/blog/2015/10/how-to-build-a-machine-learning-app-using-sparkling-water-and-apache-spark/) shown in “Build a Machine-Learning App Using Sparkling Water and Apache Spark” that shows joining of tables using Spark and then publishing a Spark RDD as an H2O Frame.  Therefore its important to ensure you only have a single Frame loaded from a file when playing in Flow land – or maybe I missed a feature in Flow?

At this point, I’m now in model option land.  I’m also going to go back and have another go with R-Studio and H2O.

“‘Ask Craig’- Determining Craigslist Job Categories with Sparkling Water” offers a 2 part [article](http://blog.h2o.ai/2015/06/ask-craig-sparkling-water/) which is worth a read.

~ by mdavey on March 16, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/)
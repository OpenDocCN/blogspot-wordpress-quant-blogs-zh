<!--yml
category: 未分类
date: 2024-05-18 05:34:54
-->

# RStudio H2O Data Munging | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/04/04/rstudio-h2o-data-munging/#0001-01-01](https://mdavey.wordpress.com/2016/04/04/rstudio-h2o-data-munging/#0001-01-01)

The following is probably already well known to [RStudio](https://www.rstudio.com/) H2O experts, but for anyone not familiar with [H2O](http://www.h2o.ai/), it may aid.

Some context to begin:  I’ve got various data sets, and want to begin to experiment with the various H2O algo’s, ideally to gain insight from the data through predictions, and how the data is clustered.  The initial data set isn’t large, but will I suspect inhibit algorithms such as deep learning.

When loading a CSV file with headers via h2o.uploadFile, make sure each column header is unique 🙂  Obvious, but not sometimes 🙂

```
data.hex &lt;- h2o.uploadFile(path = "/Users/Matt/Downloads/sampledata.csv",header = TRUE, sep = ",", destination_frame = "data.hex")

```

Colnames and summary are useful sometimes:

```
colnames(data.hex)
summary(data.hex)

```

RStudio [Tips](https://twitter.com/rstudiotips) can be useful.

Histograms can be easily displayed for a column using:

```
h2o.hist(data.hex$"&lt;column name&gt;")

```

Get to the help page of a H2O algorithm using help:

```
help(h2o.kmeans)

```

[Cross Validated](http://stats.stackexchange.com/) is a question and answer site for people interested in statistics, machine learning, data analysis, data mining, and data visualization – I’ve found it useful a few times for answers to questions.

The R H2O [tutorial](http://h2o-release.s3.amazonaws.com/h2o/rel-lambert/5/docs-website/Ruser/rtutorial.html) is helpful, but what is missing is more detail on understanding the output from the algorithms.  As an example, take the sample code for prostate.csv.  Once the Generalized linear model is applied to the dataset, more information on the output, and also the summary() output would aid beginners.  I suspect this is some book or other reading material that solve this knowledge gap.

Re-writing the prostate code for 3.8.06 H2O, leads to the following:

```
prostate.hex &lt;- h2o.importFile(path= "https://raw.github.com/0xdata/h2o/master/smalldata/logreg/prostate.csv")
data.split &lt;- h2o.splitFrame(data = prostate.hex, ratios = 0.8)
prostate.train &lt;- data.split[[1]]
prostate.test &lt;- data.split[[2]]
prostate.glm &lt;- h2o.glm(y = "CAPSULE", x = c("AGE","RACE","PSA","DCAPS"), training_frame = prostate.train, validation_frame = prostate.test,family = "binomial", nfolds = 10, alpha = 0.5)
prostate.fit &lt;- h2o.predict(object = prostate.glm, newdata = prostate.hex)
summary(prostate.fit)

```

Which provides the following output form summary():

```
predict p0 p1
Min. :0.0000 Min. :0.001468 Min. :0.1590
1st Qu.:0.0000 1st Qu.:0.538552 1st Qu.:0.2911
Median :1.0000 Median :0.663140 Median :0.3369
Mean :0.5737 Mean :0.588795 Mean :0.4112
3rd Qu.:1.0000 3rd Qu.:0.708884 3rd Qu.:0.4614
Max. :1.0000 Max. :0.840978 Max. :0.9985

```

Which based on this [posting](http://www.r-bloggers.com/things-to-try-after-user-part-1-deep-learning-with-h2o/), provides “the predicted label with the probabilities of all possible outcomes (or numeric outputs for regression problems)”

~ by mdavey on April 4, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/), [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)
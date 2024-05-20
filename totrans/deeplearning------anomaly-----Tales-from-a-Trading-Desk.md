<!--yml
category: 未分类
date: 2024-05-18 05:31:08
-->

# deeplearning() -> anomaly() | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/06/10/deeplearning-anomaly/#0001-01-01](https://mdavey.wordpress.com/2016/06/10/deeplearning-anomaly/#0001-01-01)

## deeplearning() -> anomaly()

“Anomaly [Detection](http://amunategui.github.io/anomaly-detection-h2o/): Increasing Classification Accuracy with H2O’s Autoencoder and R” offers some great ideas around using the h2o.deeplearning() algorithm to detect anomalies.

Further, a read of [this](http://www.kdnuggets.com/2015/06/decision-boundaries-deep-learning-machine-learning-classifiers.html) may aid in boundary detection, and further coolness via h2o.[feature](http://rpackages.ianhowson.com/cran/h2o/man/h2o.deepfeatures.html) [here](https://github.com/h2oai/h2o-training-book/blob/master/hands-on_training/anomaly_detection.md).

Once you’ve got your model, drop it to a [H2o](http://learn.h2o.ai/content/tutorials/deeplearning/index.html?_ga=1.212220820.145610645.1456331433) POJO if required, and hook it up to your stream of data.

~ by mdavey on June 10, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/)
Tags: [AI](https://mdavey.wordpress.com/tag/ai/), [MachineLearning](https://mdavey.wordpress.com/tag/machinelearning/)
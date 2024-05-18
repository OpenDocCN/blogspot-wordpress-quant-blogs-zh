<!--yml
category: 未分类
date: 2024-05-18 14:05:04
-->

# Introduction of SVM Learning in Strategies – Quantum Financier

> 来源：[https://quantumfinancier.wordpress.com/2010/05/21/application-of-svms/#0001-01-01](https://quantumfinancier.wordpress.com/2010/05/21/application-of-svms/#0001-01-01)

This post is derived from a comment I received my last post on probability density function for an adaptive RSI strategy. *pinner* made the following observation:

> *“Alternatively you could regress the returns against the set of 6mo & 1yr RSI points as a means to determine the best decision. While this approach probably requires more historical data, it also affords more detailed metrics from which to make each decision.”*

I am personally not a big fan of simple regression model for my trading decisions. However, I think there is something in the concept. Such a setup is also a good place to use a common traditional machine learning technique; the support vector machine (SVM).

From wikipedia: given a set of training examples, each marked as belonging to one of two categories, an SVM training algorithm builds a model that predicts whether a new example falls into one category or the other. Intuitively, an SVM model is a representation of the examples as points in space, mapped so that the examples of the separate categories are divided by a clear gap that is as wide as possible. New examples are then mapped into that same space and predicted to belong to a category based on which side of the gap they fall on.

In concrete terms, the training algorithm separate the data into up days and down days then look at the predictors value. It then creates a set of rules dividing the data; these rules minimize the classification error while also maximizing the margin of safety, thus giving the model more room, resulting (hopefully) in a greater accuracy. Based on this set of rules, the algorithm classifies new data in a category. Note that this is not a numeric prediction (i.e. next day return should be xx%) it is a binary factor prediction, thus allowing us to derive a probability along with the prediction. It comes in handy when we want a confidence based system.

This is a nice technique, but it has its drawbacks. First of all, it is a parameter dependant technique. The effectiveness of the svm is mostly determined by two parameters. It is usually recommended to test different values for the pair and to retain the pair that performs best during cross-validation for the model. This can become quite computationally annoying. Without getting to technical (or into details), if we want a non-linear classification algorithm, we have to choose the type of kernel function we want; there is several.

I just wanted to throw the idea out there, since pinner’s suggestion was a good one. If readers are interested to try it out, I encourage you to send me the results, I would be happy to post them. Alternatively, I might post some results depending on the interest. I just wanted to introduce support vector machine and its potential application when developing strategies.

QF
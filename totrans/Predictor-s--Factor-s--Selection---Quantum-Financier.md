<!--yml
category: 未分类
date: 2024-05-18 14:00:52
-->

# Predictor(s)/Factor(s) Selection – Quantum Financier

> 来源：[https://quantumfinancier.wordpress.com/2011/01/09/predictorfactor-selection/#0001-01-01](https://quantumfinancier.wordpress.com/2011/01/09/predictorfactor-selection/#0001-01-01)

Before getting in the post main subject, I want to mention a couple things. First, the TAA system talked about before on the blog is still in the works, a busy schedule and work commitment made it difficult for me to polish and publish it as soon as I wanted. Secondly, I apologize for the New Year’s hiatus; I will be back to regular posting in the coming days.

Back to the subject at hand; predictor selection. For usual readers of the blog, machine learning will not strike as an unusual topic for the blog. I really enjoy using statistical learning models for my research and trading, and talked about it a fair bit in earlier posts. However, reviewing the blog history recently, I noticed that I overlooked this very important topic.

The same way we must be careful what predictor(s) we use when using linear regression or, for that matter, any forecasting model we need to pay close attention to our input when using learning models (GIGO: garbage in = garbage out).

Using a “kitchen sink” approach and using as many predictors as one can think of is generally not the way to go. A large number of predictors often bring a high level of noise which usually makes it very hard to identify reliable patterns in the data for the models. On the other hand, with very few predictors, it is unlikely that there will be a lot of high probability patterns to profit from. In theory we are trying to minimize the number of predictors for a given accuracy level.

In practice, we usually go from what the theory suggests or discretionary observation to determine what should be included. The quantification of this process is often called Exploratory Factor Analysis (EFA); basically looking at the covariance matrix of our predictors and perform an eigenvalue decomposition. Doing this we aim to determine the number of factors influencing our response (dependant) variable, and the strength of this influence. This technique is useful to better understand the relationships between a predictor and the response variable and determine what predictors are most important when classifying. This type of covariance matrix decomposition is supposed to help us refine our predictor selection and hopefully improve classification performance; this process will be the object of the next few posts.

QF
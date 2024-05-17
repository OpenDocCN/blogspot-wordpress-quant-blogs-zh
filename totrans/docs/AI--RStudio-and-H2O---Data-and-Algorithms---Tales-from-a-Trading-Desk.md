<!--yml
category: 未分类
date: 2024-05-18 05:35:20
-->

# AI: RStudio and H2O – Data and Algorithms | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/03/18/ai-rstudio-and-h2o-data-and-algorithms/#0001-01-01](https://mdavey.wordpress.com/2016/03/18/ai-rstudio-and-h2o-data-and-algorithms/#0001-01-01)

## AI: RStudio and H2O – Data and Algorithms

Having made some progress with H2O Flow, its time to leverage [R](http://www.h2o.ai/product/integration/) using RStudio.  As I mentioned in a previous posting, the overarching of data science is ensuring you have the right data, and use the right algorithms, else you’ll get rubbish insight 🙂

I’ve found it useful to think about the questions I’m trying to answer thought AI before doing anything with data.  If the data your refining is the definitive data set, then your hands are tied 😦  If you happen to own the platform your getting the data from, then you can at least enhance data collection to aid the AI side of the equation.

Often when you start looking at the types of questions you want to answer it becomes clear very quickly that you either don’t currently have the data, or the data isn’t shaped appropriately to be ingested by the AI model.  Sometimes creating a sample test data set at least allow thought to be put into the model and the outputs – classifications, predictions etc, prior to taking real world data, and continuing to refine the model.

Few useful links:

*   Use H2O [directly](http://www.h2o.ai/download/h2o/r) from R – this is very cool, and very useful just to get going.  Further, its lighter than running H2O web server and Flow 🙂
*   H2O R [package](http://h2o-release.s3.amazonaws.com/h2o/rel-turan/3/docs-website/h2o-r/h2o_package.pdf)
*   Fast [Scalable](https://h2o-release.s3.amazonaws.com/h2o/rel-slater/9/docs-website/h2o-docs/booklets/R_Vignette.pdf) R with H2O – if you are still struggling with models, try chapter 6 of this [document](https://h2o-release.s3.amazonaws.com/h2o/rel-slater/9/docs-website/h2o-docs/booklets/R_Vignette.pdf).
*   R [Tutorial](http://h2o-release.s3.amazonaws.com/h2o/rel-kahan/2/docs-website/tutorial/rtutorial.html) – useful code extract for running models and such
*   H2O in R [Studio](http://h2o-release.s3.amazonaws.com/h2o/master/1247/docs-website/Ruser/R_studio.html)
*   [Diving](http://blog.revolutionanalytics.com/2014/04/a-dive-into-h2o.html) into H2O
*   Predict Social [Network](http://thinktostart.com/predict-social-network-influence-with-r-and-h2o-ensemble-learning/) Influence with R and H2O Ensemble Learning

Recap of [models](https://h2o-release.s3.amazonaws.com/h2o/rel-slater/9/docs-website/h2o-docs/booklets/R_Vignette.pdf):

*   Generalized Linear Models (GLM): A flexible generalization of ordinary linear regression for response variables that have error distribution models other than a normal distribution. GLM unifies various other statistical models, including linear, logistic, Poisson, and more. Decision trees: Used in RF; a decision support tool that uses a tree-like graph or model of decisions and their possible consequences.
*   Gradient Boosting (GBM): A method to produce a prediction model in the form of an ensemble of weak prediction models. It builds the model in a stage-wise fashion and is generalized by allowing an arbitrary differentiable loss function. It is one of the most powerful methods available today.
*   K-Means: A method to uncover groups or clusters of data points often used for segmentation. It clusters observations into k certain points with the nearest mean.
    Anomaly Detection: Identify the outliers in your data by invoking a powerful pattern recognition model, the Deep Learning Auto-Encoder.
*   Deep Learning: Model high-level abstractions in data by using non-linear transformations in a layer-by-layer method. Deep learning is an example of supervised learning and can make use of unlabeled data that other algorithms cannot.
*   Naıve Bayes: A probabilistic classifier that assumes the value of a particular feature is unrelated to the presence or absence of any other feature, given the class variable. It is often used in text categorization.
*   Grid Search: The standard way of performing hyper-parameter optimization to make model configuration easier. It is measured by cross-validation of an independent data set.

~ by mdavey on March 18, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/)
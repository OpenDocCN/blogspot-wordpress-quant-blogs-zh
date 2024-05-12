<!--yml
category: 未分类
date: 2024-05-12 17:42:04
-->

# Current S&P500 Economic Forecasting Model Prediction | CSSA

> 来源：[https://cssanalytics.wordpress.com/2019/05/27/current-sp500-economic-forecasting-model-prediction/#0001-01-01](https://cssanalytics.wordpress.com/2019/05/27/current-sp500-economic-forecasting-model-prediction/#0001-01-01)

We introduced our [machine-learning economic forecasting model](https://cssanalytics.wordpress.com/2019/05/14/shiny-new-toys/) as a neat new way to compress a ton of economic data to gauge the health of the economy in order to predict cyclical (not sentiment driven) drawdowns in the stock market. The current prediction uses two different models:

1) **Composite Point-in-time**– this model only creates a forecast when all data required by the model is available at the point-in-time that it was available. If the model is waiting on data it will simply carry forward the last prediction made when all data was available. The [historical prediction table](https://cssanalytics.wordpress.com/2019/05/15/current-sp500-economic-forecasting-model-introduction/) was generated using this model.

2) **Preliminary** – this model is trained using the data available and is capable of making forecasts when there is missing data that the Composite model is waiting for. It does this by interpolating the missing data. Currently given that there are three missing pieces of data we can only make a preliminary forecast through the end of June.

## Current Prediction- Preliminary

For the prediction period **Apr 2019 – Jun 2019**, the model predicts the following results based on economic data as of **Mar 31, 2019**:

*   Is there a reasonable chance of a large correction happening between Apr 2019 – Jun 2019? **Not Expected**
*   What is the predicted direction of returns between Apr 2019 – Jun 2019? **Flat**
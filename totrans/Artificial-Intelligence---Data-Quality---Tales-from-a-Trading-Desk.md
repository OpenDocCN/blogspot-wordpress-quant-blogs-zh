<!--yml
category: 未分类
date: 2024-05-18 05:30:47
-->

# Artificial Intelligence – Data Quality | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/06/23/artificial-intelligence-data-quality/#0001-01-01](https://mdavey.wordpress.com/2016/06/23/artificial-intelligence-data-quality/#0001-01-01)

## Artificial Intelligence – Data Quality

Most corporations as soon as they venture down the road of “big data”, and AI, realise they often don’t have a big data issue, they have a data quality issue, which is probably coupled to data holes within the corporate data set.  This is driven by a number of issues, including:

*   No Chief Data Officer
*   No Data Strategy
*   Lack of thought as to how the data from a application (division, department etc) will be used outside of the application (User Experience) itself
*   No Acceptance Criteria on stories around data quality

Data hygiene is key to deriving using predictions and classifications from AI [models](http://www.h2o.ai/) – obvious 🙂

What follows are a few pointers that may aid in the area of data hygiene:

*   Identification of source of truth (SoT) of data e.g. market data, trades, orders, recruitment.  Using a secondary copy of the SoT can often lead to “issues”
*   Context around data changes in the SoT.  Specifically, who changed what, when, and ideally why.  “Why” can be difficult in certain instances, but ideally would provide some context on the path that lead to a data change e.g phone call from a client requesting an amendment to a trade
*   Taxonomy/ontology – if you are doing anything around LDA to extract topics, then its going to help considerably if the input data leverages a taxonomy to reduce the surface area of data.
*   Applications are often built with no thought around any of the above points.  Further, if you are using ELK or similar as a data source for AI models, its will not be uncommon to find that application development didn’t consider the logs during development 😦  In this scenario, I’d advise mandating ELK to development teams 🙂  At a minimum, this will aid the reduction of support tickets as support staff will at least have meaningful log files to work with 🙂

Its truly amazing how time can be wasted prior to training AI models with cleaning and collecting data 😦

~ by mdavey on June 23, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/), [Trading](https://mdavey.wordpress.com/category/trading/)
Tags: [AI](https://mdavey.wordpress.com/tag/ai/), [MachineLearning](https://mdavey.wordpress.com/tag/machinelearning/)
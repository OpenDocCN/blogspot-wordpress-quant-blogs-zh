<!--yml
category: 未分类
date: 2024-05-18 05:45:28
-->

# 21st Century Pricing Engines | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2014/10/22/21st-century-pricing-engines/#0001-01-01](https://mdavey.wordpress.com/2014/10/22/21st-century-pricing-engines/#0001-01-01)

## 21st Century Pricing Engines

In todays markets, there are a number of drives that influence the buy vs build of a pricing engine irrespective of asset class.  Those drives probably include the following:

*   Consistent pricing
*   Minimising the number of trade away %
*   Ability to on-boarding clients in a timely manner
*   High availability, low latency of both price construction, and price delivery

This leads to a number of requirements which i suspect maybe mandatory in certain organisations:

*   Liquidity steam per user (not client) sourced from a liquidity pool – historical 3-5 tier pricing probably isn’t good enough these days
*   High availability – consistent pricing from multi data centres
*   Injection of [CIV](http://www.headforpoints.com/2014/06/09/british-airways-civ-score-corporate-individual-value/) to influence price construction
*   Ingestion of order and traded away data to improve the core price generation
*   Parameter driven configuration
*   Influenced by the latency from end to end – slow/fast consuming clients

Which then leads to the questions, do you build or buy an off the shelf product.

~ by mdavey on October 22, 2014.

Posted in [Trading](https://mdavey.wordpress.com/category/trading/)
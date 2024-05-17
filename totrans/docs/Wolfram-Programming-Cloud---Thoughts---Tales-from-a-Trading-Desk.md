<!--yml
category: 未分类
date: 2024-05-18 05:48:36
-->

# Wolfram Programming Cloud – Thoughts | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2014/06/24/wolfram-programming-cloud-thoughts/#0001-01-01](https://mdavey.wordpress.com/2014/06/24/wolfram-programming-cloud-thoughts/#0001-01-01)

## Wolfram Programming Cloud – Thoughts

Wolfram Programming Cloud is now [live](http://blog.wolfram.com/2014/06/23/wolfram-programming-cloud-is-live/).  There is a cloud [gallery](http://www.wolfram.com/language/gallery/) providing a range of simple samples which is a good start.  There is quite a lot of documentation which is a good start.  Having not spend enough time on Wolfram or read enough documentation, I’m wondering how best to leverage its feature set in both the buy and sell space:

*   Universal Database Connectivity ([UDC](http://www.wolfram.com/technology/guide/UniversalDatabaseConnectivity/)) – assume I can leverage this to connect to a risk/position data repository?
*   Import and Export [function](http://reference.wolfram.com/mathematica/tutorial/ImportingAndExportingData.html) are provide which is helpful
*   Given the plot histories of stock prices [sample](http://www.wolfram.com/language/gallery/plot-histories-of-stock-prices/), I’m guessing by leveraging UDC, one can plot the same by using the UDC data source
*   Can I connect my [InfluxDB](http://influxdb.com/docs/v0.7/introduction/overview.html) to Wolfram given InfluxDB has time series data, and Wolfram has TimeSeries functionality?

~ by mdavey on June 24, 2014.

Posted in [Cloud](https://mdavey.wordpress.com/category/hpc/cloud/)
Tags: [Wolfram](https://mdavey.wordpress.com/tag/wolfram/)
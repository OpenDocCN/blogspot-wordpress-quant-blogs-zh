<!--yml
category: 未分类
date: 2024-05-18 06:23:31
-->

# Tibco (StreamBase) and Software AG (Apama) Thoughts | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2013/06/17/tibco-streambase-and-software-ag-apama-thoughts/#0001-01-01](https://mdavey.wordpress.com/2013/06/17/tibco-streambase-and-software-ag-apama-thoughts/#0001-01-01)

## Tibco (StreamBase) and Software AG (Apama) Thoughts

Wall Street & Technology offers a [view](http://www.wallstreetandtech.com/it-infrastructure/whats-behind-the-cep-buying-spree/240156739) on the recent CEP buying spree.  My view is that from a financial services perspective, having low latency messaging bus that connects active [in-memory](http://www.benstopford.com/data-grids-with-oracle-coherence-an-introduciton/) data nodes is the first cornerstone for a real-time big data [risks](http://www.gigaspaces.com/content/massively-scalable-real-time-risk-analysis-webinar) analysis platform – data messaging fabric 🙂  Mix in a distributed Complex Event Processing (CEP) component that offer both pre-define, and dynamic aggregation and computation of data for both real-time and bi-temporal data sets.

Clearly this product will need a super cool User Interface (UI), which leads to Bret Victor ([as](http://www.righto.com/2011/12/javascript-secrets-of-worrydreamcom.html) blogged [previous](https://github.com/worrydream/Tangle)), and Tangle, which would allow this [super](http://danielhooper.tumblr.com/post/19313911658/codebook) [cool](http://danielchasehooper.github.io/CodeBook/) UI to interact with the dynamic event processing server side component, [varying](http://livecoding.io/) the inputs that form the basis for the data presented.

~ by mdavey on June 17, 2013.

Posted in [Cloud](https://mdavey.wordpress.com/category/hpc/cloud/)
Tags: [BigData](https://mdavey.wordpress.com/tag/bigdata/), [CEP](https://mdavey.wordpress.com/tag/cep/), [Risk](https://mdavey.wordpress.com/tag/risk/)
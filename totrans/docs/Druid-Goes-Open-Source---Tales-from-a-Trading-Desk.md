<!--yml
category: 未分类
date: 2024-05-18 06:34:11
-->

# Druid Goes Open Source | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2012/10/29/druid-goes-open-source/#0001-01-01](https://mdavey.wordpress.com/2012/10/29/druid-goes-open-source/#0001-01-01)

## Druid Goes Open Source

Interesting to see that MetaMarkets has [pushed](http://metamarkets.com/2012/metamarkets-open-sources-druid/) Druid into the Open Source world.  The history of Druid is interesting, specifically the path MetaMarkets went down prior to building Druid.

What’s particularly nice about Druid is distributed in-memory data engine, allows JavaScript clients to retrieve real-time data – I’m [assuming](http://metamarkets.com/platform/) “Event data can be streamed live” [means](http://metamarkets.com/2011/node-js-and-the-javascript-age/) web push via [Node.js](http://metamarkets.com/2012/node-js-for-the-enterprise/)
Druid features:

*   **Distributed architecture. **Swappable read-only data segments using an MVCC swapping protocol. Per-segment replication relieves load on hot segments. Supports both in-memory and memory-mapped versions.
*   **Real-time ingestion. **Real-time ingestion coupled with broker servers to query across real-time and historical data. Automated migration of real-time to historical as it ages.
*   **Column-oriented for speed. ** Data is laid out in columns so that scans are limited to specific data being searched. Compression decreases overall data footprint.
*   **Fast filtering. **Bitmap indices with CONCISE compression.
*   **Operational simplicity. **Fault tolerant due to replication. Supports rolling deployments and restarts. Allows simple scale up and scale down – just add or remove nodes.

So net out, Druid sound interesting for all of the above from a technical perspective, and from a business perspective  for possibly real-time risk and e-Commerce sales intelligence analysis and visualization

~ by mdavey on October 29, 2012.

Posted in [JavaScript](https://mdavey.wordpress.com/category/languages/javascript/)
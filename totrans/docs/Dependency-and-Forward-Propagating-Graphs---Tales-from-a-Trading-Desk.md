<!--yml
category: 未分类
date: 2024-05-18 05:58:14
-->

# Dependency and Forward-Propagating Graphs | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2013/11/11/dependency-and-forward-propagating-graphs/#0001-01-01](https://mdavey.wordpress.com/2013/11/11/dependency-and-forward-propagating-graphs/#0001-01-01)

## Dependency and Forward-Propagating Graphs

Although I’ve blogged about Athena before, its worth a re-read of Athena from the JPM [careers](http://techcareers.jpmorgan.com/cm/BlobServer/athena_jpmc.pdf?blobkey=id&blobwhere=1320615212303&blobheader=application/pdf&blobheadername1=Cache-Control&blobheadervalue1=private&blobcol=urldata&blobtable=MungoBlobs) data.

> Dependency graph – developers define specially decorated Python classes to represent markets, financial instruments and deals. A runtime parser inspects the classes to build an in-memory
> 
> [dependency](http://bigblog.tanbin.com/2010/11/secdb-schemaless-graph-database.html)
> 
> graph representing the relationships between them. This provides a natural and powerful way to explore ‘what-if’ scenarios by moving market rates and examining the impact on prices derived from them.
> 
> At the core of the (athena reactive) framework is a forward-propagating graph, where nodes contain units of work scheduled forexecution based on their ranking (topologically sorted order) in the graph.

~ by mdavey on November 11, 2013.

Posted in [Languages](https://mdavey.wordpress.com/category/languages/)
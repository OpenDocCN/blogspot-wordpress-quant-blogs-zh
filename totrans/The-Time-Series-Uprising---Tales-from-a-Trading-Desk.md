<!--yml
category: 未分类
date: 2024-05-18 06:22:33
-->

# The Time-Series Uprising | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2013/07/12/the-time-series-uprising/#0001-01-01](https://mdavey.wordpress.com/2013/07/12/the-time-series-uprising/#0001-01-01)

## The Time-Series Uprising

Ben over on O’Reilly has an interesting [article](http://strata.oreilly.com/2013/04/the-re-emergence-of-time-series.html) on time-services databases.  Historically [OneTick](http://www.onetick.com/web1/onetick_accelerator.php) and [kdb](http://kx.com/kdb-plus-tick.php) have been the database’s of choice in financial services.

[OpenTSDB](http://opentsdb.net/index.html) looks interesting, given that its at least move past v1.0, but doesn’t have a streaming API – something that kdb has.

SciDB has been around for some time, and offers the following in the time-series context:

> Time [series](http://www.scidb.org/HTMLmanual/13.6/scidb_ug/ch01.html) and spatial grids may be represented in relations, but only at a severe cost in both space and processing time. SciDB will be organized around multidimensional array storage, a generalization of relational tables that can provide orders of magnitude better performance.

Although SciDB has a number of [use](http://www.scidb.org/use/) cases on its web site, none are from the financial domain – either due to confidentiality, or because it doesn’t align with financial problems.

TempoDB offer a list of customers already using the product.  REST appears to be the “API” of choice.  Curious to see TempoDB available on [Heroku](https://addons.heroku.com/tempodb).  Shame no sample visualization’s are [offered](https://www.tempo-db.com/features/#Visualization) 😦

Ben has missed [Datomic](http://www.datomic.com/), the Clojure the a database offering flexible, time-based facts, supporting queries and joins, with elastic scalability, and ACID transactions.

Anyway, curious if anyone has started to use any of the above in finance

~ by mdavey on July 12, 2013.

Posted in [Uncategorized](https://mdavey.wordpress.com/category/uncategorized/)
Tags: [Time-Series](https://mdavey.wordpress.com/tag/time-series/)
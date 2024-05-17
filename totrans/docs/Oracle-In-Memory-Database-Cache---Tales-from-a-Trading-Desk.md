<!--yml
category: 未分类
date: 2024-05-18 06:01:17
-->

# Oracle In-Memory Database Cache | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2013/09/24/oracle-in-memory-database-cache/#0001-01-01](https://mdavey.wordpress.com/2013/09/24/oracle-in-memory-database-cache/#0001-01-01)

## Oracle In-Memory Database Cache

The tech news wires are a [flutter](http://www.eweek.com/database/oracle-details-12c-database-exadata-x3-new-cloud-services/) with Larry Ellison’s keynote at [OpenWorld](http://www.oracle.com/openworld/index.html).  Of particular interest is the [in-memory](http://www.forbes.com/sites/alexkonrad/2013/09/23/oracle-announces-in-memory-at-openworld/) database feature of [12C](http://www.oracle.com/technetwork/database/oracle-database-editions-wp-12c-1896124.pdf):

> Oracle In-Memory Database Cache enables you to improve application transaction response times and throughput by caching performance-critical subsets of an Oracle Database in the application tier. The Oracle In-Memory Database Cache (IMDB Cache) option of Oracle Database 12c caches and processes data in the memory of the applications themselves; off-loading the data processing to middle tier resources. With Oracle Database 12c, the ability to transparently deploy IMDB Cache with existing Oracle applications becomes much easier – with common data types, SQL and PL/SQL support, and native support for the Oracle Call Interface (OCI).

So clearly the obvious question given the above is; if your software stack today leverages Oracle Coherence in front of an Oracle DB, can you with 12C, throw away Coherence, and gain all the benefits of Coherence with the 12C in-memory feature set?  I suspect [Continuous](http://docs.oracle.com/cd/E15357_01/coh.360/e15723/api_continuousquery.htm) Query’s are not supported by 12C?

~ by mdavey on September 24, 2013.

Posted in [Cloud](https://mdavey.wordpress.com/category/hpc/cloud/)
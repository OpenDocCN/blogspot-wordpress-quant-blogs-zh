<!--yml

类别：未分类

日期：2024-05-18 06:01:17

-->

# Oracle In-Memory Database Cache | Tales from a Trading Desk

> 来源：[`mdavey.wordpress.com/2013/09/24/oracle-in-memory-database-cache/#0001-01-01`](https://mdavey.wordpress.com/2013/09/24/oracle-in-memory-database-cache/#0001-01-01)

## Oracle In-Memory Database Cache

科技新闻线[纷飞](http://www.eweek.com/database/oracle-details-12c-database-exadata-x3-new-cloud-services/)，拉里·埃里森在[OpenWorld](http://www.oracle.com/openworld/index.html)的演讲。特别值得注意的是[12C](http://www.oracle.com/technetwork/database/oracle-database-editions-wp-12c-1896124.pdf)的[内存中](http://www.forbes.com/sites/alexkonrad/2013/09/23/oracle-announces-in-memory-at-openworld/)数据库功能：

> Oracle In-Memory Database Cache 使您能够通过在应用程序层缓存 Oracle 数据库的性能关键子集来提高应用程序事务响应时间和吞吐量。Oracle Database 12c 的 Oracle In-Memory Database Cache（IMDB Cache）选项在应用程序自身的内存中缓存和处理数据；将数据处理卸载到中间层资源。有了 Oracle Database 12c，能够透明地与现有的 Oracle 应用程序部署 IMDB Cache 变得容易得多——支持常见数据类型、SQL 和 PL/SQL，以及原生支持 Oracle 调用接口（OCI）。

因此，显然根据上述内容，一个明显的问题就是；如果你的软件堆栈今天在 Oracle DB 前使用 Oracle Coherence，那么在 12C 中，你可以扔掉 Coherence，并利用 12C 内存功能集合获得 Coherence 的所有好处吗？我怀疑[连续查询](http://docs.oracle.com/cd/E15357_01/coh.360/e15723/api_continuousquery.htm)是否支持 12C？

~ mdavey 于 2013 年 9 月 24 日。

发布在[云](https://mdavey.wordpress.com/category/hpc/cloud/)

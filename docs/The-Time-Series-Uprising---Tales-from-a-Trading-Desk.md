<!--yml

分类：未分类

日期：2024-05-18 06:22:33

-->

# 时间序列起义 | 交易桌旁的传说

> 来源：[`mdavey.wordpress.com/2013/07/12/the-time-series-uprising/#0001-01-01`](https://mdavey.wordpress.com/2013/07/12/the-time-series-uprising/#0001-01-01)

## 时间序列起义

O’Reilly 的 Ben 写了一篇有趣的[文章](http://strata.oreilly.com/2013/04/the-re-emergence-of-time-series.html)关于时间序列数据库。历史上[OneTick](http://www.onetick.com/web1/onetick_accelerator.php)和[kdb](http://kx.com/kdb-plus-tick.php)一直是金融服务业的首选数据库。

来源：[OpenTSDB](http://opentsdb.net/index.html)看起来很有趣，毕竟它已经至少超过了 v1.0，但它没有流式 API——这是 kdb 所拥有的。

SciDB 已经存在一段时间，并在时间序列上下文中提供以下功能：

> 时间[序列](http://www.scidb.org/HTMLmanual/13.6/scidb_ug/ch01.html)和空间网格可以在关系中表示，但这样做在空间和处理时间上的代价非常高。SciDB 将围绕多维数组存储组织，这是关系表的泛化，可以提供更好的性能。

尽管 SciDB 在其网站上有很多[用途](http://www.scidb.org/use/)案例，但没有一个是来自金融领域的——这可能是由于保密，或者它与金融问题不匹配。

TempoDB 列出了已经使用该产品的客户。REST 似乎是“API”的首选。好奇看到 TempoDB 可以在[Heroku](https://addons.heroku.com/tempodb)上使用。遗憾没有提供样本可视化 😦

Ben 没有提到[Datomic](http://www.datomic.com/)，这是一个 Clojure 数据库，提供灵活的时间事实，支持查询和连接，具有弹性可扩展性和 ACID 事务。

无论如何，好奇是否有人已经在金融领域开始使用上述工具

~ mdavey 于 2013 年 7 月 12 日。

发布于[未分类](https://mdavey.wordpress.com/category/uncategorized/)

标签：[时间序列](https://mdavey.wordpress.com/tag/time-series/)

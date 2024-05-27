<!--yml

类别：未分类

日期：2024-05-18 05:32:33

-->

# 语义数据模型 | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2016/05/09/semantic-data-model/#0001-01-01`](https://mdavey.wordpress.com/2016/05/09/semantic-data-model/#0001-01-01)

## 语义数据模型

当 Hadoop 不够用时：“When Hadoop Simply Isn’t Enough: How to Purpose-Build Architecture for Industrial Data”提供了一个有趣的[阅读](http://insidebigdata.com/2015/12/07/when-hadoop-simply-isnt-enough-how-to-purpose-build-architecture-for-industrial-data/)，但并未提到 RDF 的。ElasticSearch 和 Hadoop 被提及为解决方案的一部分，但我并不清楚数据是如何链接的。我错过了什么吗？

“数据湖概念正在[成熟](http://cacm.acm.org/news/200095-the-data-lake-concept-is-maturing/fulltext)”，然而提供了更有趣的阅读，其中 Apache Hadoop 分布式文件系统被指出用于存储，与以下内容结合：

> 当选择一个 NoSQL 数据库与他们的 Hadoop 集群工作时，MongoDB 通常用于部门级别的缓存应用，Apache Cassandra 用于高度分布式交互应用，而 Apache [Hbase](https://hbase.apache.org/)用于分析应用，Bodkin 说“可以容忍更多的延迟，机器学习模型在 Hadoop 计算集群旁边有更少的地方”。

从[Graph](http://www.snee.com/bobdc.blog/2014/01/storing-and-querying-rdf-in-ne.html)数据库的角度来看，一篇关于[Neo4j](http://michaelbloggs.blogspot.co.uk/2013/05/importing-ttl-turtle-ontologies-in-neo4j.html)和 RDF 的有趣文章，“在 Neo4j 中导入 ttl（Turtle）本体论”。

关于 Sempala 的研究很有趣，但我没在任何地方看到代码。

最后，关于[Spark](http://www.snee.com/bobdc.blog/2015/03/spark-and-sparql-rdf-graphs-an.html)和 SPARQL，“RDF 图和[GraphX](http://www.snee.com/bobdc.blog/2015/03/spark-and-sparql-rdf-graphs-an.html)“。

这仍然导致了一个问题：最新的数据湖软件堆栈是什么？通往[HBase](http://hbase.apache.org/book.html#arch.overview)的道路是否要持有[数据](http://www.tutorialspoint.com/hbase/hbase_create_data.htm)和/或 RDF 的？[Jena-HBase](http://ceur-ws.org/Vol-914/paper_14.pdf) 或者 HBase 与一个单独的图[数据库](http://www.datanami.com/2015/05/26/hadoop-triple-stores-and-the-semantic-data-lake/)结合提供 SPARQL 查询？

~ mdavey 于 2016 年 5 月 9 日。

发布在[数据](https://mdavey.wordpress.com/category/data/)类别下

标签：[DataLake](https://mdavey.wordpress.com/tag/datalake/)，[Ontology](https://mdavey.wordpress.com/tag/ontology/)

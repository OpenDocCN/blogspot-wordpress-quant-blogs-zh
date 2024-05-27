<!--yml

类别: 未分类

日期: 2024-05-18 05:32:46

-->

# 数据湖：选择哪种 RDF 数据存储？ | 来自一个交易台的故事

> 来源：[`mdavey.wordpress.com/2016/05/03/which-rdf-data-store/#0001-01-01`](https://mdavey.wordpress.com/2016/05/03/which-rdf-data-store/#0001-01-01)

## 数据湖：选择哪种 RDF 数据存储？

这里列出了许多三元组存储器 [here](https://www.w3.org/2001/sw/wiki/Java)。  GraphDB 看起来 [interesting](http://graphdb.ontotext.com/graphdb/)，但我怀疑企业版会倾向于开源解决方案。  在大数据的世界中，我怀疑你真的想要 SPARSQL 而不是 [Hadoop](https://jena.apache.org/documentation/hadoop/)？

> 将数据存储在 Hadoop 的键值存储中 [Hbase]，然后用我们的 [图形](http://www.datanami.com/2015/05/26/hadoop-triple-stores-and-the-semantic-data-lake/) 数据库对其进行索引，以便我们可以执行这些 SPARQL 查询

这由“避免数据湖的三个常见 [陷阱](http://data-informed.com/avoiding-three-common-pitfalls-data-lakes/)”所引用：

> 智能数据技术大大降低了数据湖实施的复杂性，同时加快了它们产生价值的时间。基于图形的模型和数据元素的详细描述大大增强了集成工作，使业务用户能够根据提供关键背景的相关属性链接数据，跨数据源和业务模型。资源描述框架（RDF）图旨在在不必重新配置现有表示的情况下纳入新数据和源。结果是大大缩短了达到更深层次分析的时间，在这种分析中，用户不仅可以比以前更迅速地提出更多问题，而且还可以确定关系和数据背景以针对特定需求发出特定的即席查询。

虽然较老，但仍然有趣“在 [NoSQL](http://www.snee.com/bobdc.blog/2013/12/storing-and-querying-rdf-in-no.html) 数据库管理器中存储（和查询）RDF”

> 然后，本文描述了使用 HBase 和 Jena 进行查询的 RDF 的存储和查询，使用 HBase 和 Hive 作为查询引擎（使用 Jena 的 ARQ 在将其转换为 HiveQL 之前解析查询），CumulusRDF（Cassandra with Sesame）和 Couchbase

这导致了以下可能的选项：

+   用于索引您的数据湖的 RDF 数据存储

+   在您的数据湖之上使用 [D2R](http://d2rq.org/)

有人有看法吗？

~ 作者 mdavey，2016 年 5 月 3 日。

发布在 [Data](https://mdavey.wordpress.com/category/data/) 中

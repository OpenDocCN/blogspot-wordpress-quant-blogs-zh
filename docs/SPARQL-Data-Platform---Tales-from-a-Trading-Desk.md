<!--yml

分类：未分类

日期：2024-05-18 05:32:29

-->

# SPARQL 数据平台 | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2016/05/10/sparql-data-platform/#0001-01-01`](https://mdavey.wordpress.com/2016/05/10/sparql-data-platform/#0001-01-01)

## SPARQL 数据平台

鉴于最近关于 SPARQL 的各种文章，我认为记录下我考虑过的各种数据平台选项是值得的：

1.  对于纯粹的 PoC，MySQL 使用 MySQLWorkbench 中的文件导入功能，运行 [D2RQ](http://d2rq.org/getting-started) 以提供 SPARQL 访问。简单，易于设置。

1.  对于更像是 Hadoop 平台的，[HBase](https://hbase.apache.org/) 与 Apache [Phoenix](https://phoenix.apache.org/) 提供 JDBC 驱动程序，再次允许 D2RQ 用作 SPARQL 访问层。

1.  Apache [Marmotta](http://marmotta.apache.org/)，在许多方面是上述选项 1 的改进，因为它基于标准 [数据库](http://marmotta.apache.org/installation.html) 技术。

选项 1 可能是进展最快的，一旦你厌倦了访问分散在 n 个系统中的企业数据，并且你仍然在机器学习发现领域🙂 如果 you’ve 使用 Apache Marmotta，或者有时间为它设置并学习平台，选项 3 可能是一个更好的选择。

选项 2 可能是生产版本，或者至少是朝着正确方向的一次尝试，因为它在扩展性方面提供了改进，伴随着 Hadoopness 😄

这一切将走向何方？ “[SPARQL](http://www.r-bloggers.com/sparql-with-r-in-less-than-5-minutes/) 与 R 语言在 5 分钟内” 提供了一个快速而有趣的阅读，介绍了 SPARQL 的强大功能。如果你在构建一个没有基础（本体论）的数据湖，你可能错过了一个技巧。

对其他人任何其他选项感兴趣

~ mdavey 于 2016 年 5 月 10 日。

发布在 [数据](https://mdavey.wordpress.com/category/data/) 分类

标签：[数据湖](https://mdavey.wordpress.com/tag/datalake/)，[本体论](https://mdavey.wordpress.com/tag/ontology/)，[RDF](https://mdavey.wordpress.com/tag/rdf/)

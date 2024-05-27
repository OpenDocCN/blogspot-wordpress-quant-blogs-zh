<!--yml

类别：未分类

日期：2024-05-18 05:33:11

-->

# 语义数据湖|交易台的故事

> 来源：[`mdavey.wordpress.com/2016/04/28/semantic-data-lake/#0001-01-01`](https://mdavey.wordpress.com/2016/04/28/semantic-data-lake/#0001-01-01)

## 语义数据湖

继续在数据湖的道路上前进，Kafka [Connect](http://www.confluent.io/blog/how-to-build-a-scalable-etl-pipeline-with-kafka-connect) 从一种向数据湖喂数据的方式来看非常有趣。这导致了“[数据](http://xlime.eu/images/Deliverables/xLiMe_D1.2_Prototype_of_Data_Processing_Infrastructure.pdf)处理基础设施”的原型，以及 RDF 和 CumulusRDF 的使用。RDF 之所以有趣，是因为它因[SPARQL](https://en.wikipedia.org/wiki/SPARQL)——语义网而得到了采用。

进一步在网上搜索，找到了一个在数据分析领域非常有趣的文章，“使用 Apache Spark 进行高级实时医疗[分析](https://www.linkedin.com/pulse/advanced-real-time-healthcare-analytics-apache-spark-joel-amoussou)”。幸运的是，该文章提供了一个适当的架构图，很好地使用了 Apache Kafka。更有趣的是，它使用了本体论：

> 该架构是混合的，还包括一个生产规则引擎和一个本体推理器。这是为了利用来自基于证据的临床实践指南（CPGs）和生物医学本体如 SNOMED 的现有临床领域知识。这种方法补充了机器学习算法在不确定性下进行临床决策的概率方法。生产规则系统可以将 CPGs 转换为可执行的规则，这些规则与临床过程（工作流程）和事件完全集成。Drools 支持正向和反向链式以及用业务流程建模符号（BPMN）建模业务流程（临床工作流程）。有将规则和过程集成的模式。

有趣的是，有一个 W3C 机器学习架构社区[小组](https://www.w3.org/community/ml-schema/)——RDF 等。在机器学习和本体工程网站上还有一个[项目](http://aksw.org/Groups/MOLE.html)列表。

接下来，我们发现“Hadoop、三元[存储](http://www.dataversity.net/data-lakes-get-smart-with-semantic-graph-models/)、以及[语义](http://www.datanami.com/2015/05/26/hadoop-triple-stores-and-the-semantic-data-lake/)数据[湖](http://allegrograph.com/semantic-data-lake/)”：

> 我们现在投资时间最多的是语义数据湖，在那里我们在 Hadoop [Hbase]中以键值对的形式存储数据，然后用我们的图数据库对其进行索引，这样我们就可以进行这些 SPARQL 查询，

~ 由 mdavey 于 2016 年 4 月 28 日发表。

发布在[数据](https://mdavey.wordpress.com/category/data/)

标签：[DataLake](https://mdavey.wordpress.com/tag/datalake/)，[Ontology](https://mdavey.wordpress.com/tag/ontology/)

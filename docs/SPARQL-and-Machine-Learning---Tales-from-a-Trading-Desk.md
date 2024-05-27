以下是 YAML 格式的部分：

分类：未分类

日期：2024-05-18 05:32:58

以下是 YAML 格式的结束部分：

# SPARQL 和机器学习|交易桌上的故事

> 来源：[`mdavey.wordpress.com/2016/04/29/sparql-and-machine-learning/#0001-01-01`](https://mdavey.wordpress.com/2016/04/29/sparql-and-machine-learning/#0001-01-01)

## SPARQL 和机器学习

如前所述，随着行业趋势似乎正走向语义数据湖之路，了解语义机器学习的投资回报率（ROI）可能是值得的：

+   今天，遵循[CRISP-DM](https://en.wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining)过程，或者至少是类似的过程，花在理解数据上的时间相当多，并且将不同的数据集链接在一起以创建适当的数据框架（H2OFrame 等），然后你才能开始训练模型和调整模型参数。语义数据湖至少可以减少数据链接的识别时间

+   将原始数据消费到数据湖中是可以的，因为数据损失为零——ELT 而不是 ETL。然而，随着数据科学团队资源的改变，关于数据的学习时间有一定的“学习”时间。RDF 和本体论应该可以减少这个时间。

+   从数据湖的[EL](http://wortschatz.uni-leipzig.de/~fwitschel/papers/ekaw10.pdf)角度来看，[本体匹配](http://homes.cs.washington.edu/~pedrod/papers/hois.pdf)可能相当有趣——减少了在数据湖中利用新数据源的时间。

+   由于你的数据湖下面是 RDF，数据科学家现在有了一个程度的链接解析。这在不到 5 分钟的时间内简要讨论了如何在[SPARQL 与 R](http://www.r-bloggers.com/sparql-with-r-in-less-than-5-minutes/)中结合使用：

> 在我们的查询中，我们说：“给我定义在“fires”，“acres”和“year”属性的值”

我认为这篇文章中的关键语句是：

> 随着更多数据以 RDF 格式出现，自动挖掘和分析语义网的解决方案将变得越来越有用。

这使我们想起了需要一个由[RDF](https://en.wikipedia.org/wiki/SPARQL)支撑的数据湖，正如网络上的其他地方所讨论的那样。例如，如果你的数据湖正在消费社交网络数据（如 Facebook），那么你可能想看看朋友的朋友([FOAF](http://www.foaf-project.org/))，因为这将允许你利用 FOAF 本体查询（[查询](https://www.w3.org/TR/2012/WD-sparql11-overview-20120501/#sparql11-query)）湖中的多个数据源（许多数据源）

```
PREFIX foaf: &lt;http://xmlns.com/foaf/0.1/&gt;
SELECT ?name (COUNT(?friend) AS ?count)
WHERE {
    ?person foaf:name ?name .
    ?person foaf:knows ?friend .
} GROUP BY ?person ?name

```

有谁在使用[三元存储](http://jena.apache.org/)作为他们数据湖的一部分？如果有，你是如何将它与正常的 Hadoop/HDFS 数据湖世界技术结合使用的？

~ mdavey 于 2016 年 4 月 29 日。

发布在[数据](https://mdavey.wordpress.com/category/data/)分类下

标签：[机器学习](https://mdavey.wordpress.com/tag/machinelearning/)，[本体论](https://mdavey.wordpress.com/tag/ontology/)，[RDF](https://mdavey.wordpress.com/tag/rdf/)

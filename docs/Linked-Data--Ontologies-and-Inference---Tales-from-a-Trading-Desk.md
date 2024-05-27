<!--yml

分类：未分类

日期：2024-05-18 05:31:55

-->

# 链接数据、本体论和推理 | 交易桌边的传说

> 来源：[`mdavey.wordpress.com/2016/05/17/linked-data-ontologies-and-inference/#0001-01-01`](https://mdavey.wordpress.com/2016/05/17/linked-data-ontologies-and-inference/#0001-01-01)

## 链接数据、本体论和推理

虽然有些年头了，但英国博物馆的一位开发经理的这次演讲提供了一些有趣的[阅读](http://www.slideshare.net/BarryNorton/linked-data-ontologies-and-inference)。

这很好地引出了[ModelD2RQ](http://d2rq.org/jena)：

> [ModelD2RQ](http://d2rq.org/javadoc/de/fuberlin/wiwiss/d2rq/jena/ModelD2RQ.html)类为 D2RQ 映射的数据库中的数据提供了一个 Jena 模型的视图。

使用 ModelD2RQ 引擎的一个 SPARQL 查询的示例[在这里](http://d2rq.org/jena#sparql)。在互联网上快速搜索导致了一个有趣的讨论，使用了类似的[代码](https://sourceforge.net/p/d2rq-map/mailman/message/22543261/)，但围绕 D2RQ 和蕴含（有些过时），展示了使用 ModelFactory.createOntologyModel()的用法。

[ModelFactory](https://jena.apache.org/documentation/javadoc/jena/org/apache/jena/rdf/model/ModelFactory.html)看起来我们现在有了在底层数据源和请求的 SPARQL 之间添加[推理器](https://jena.apache.org/documentation/javadoc/jena/org/apache/jena/reasoner/Reasoner.html)的选项。有趣。我猜下面的代码会取得一些有趣的结果：

```
&lt;pre&gt;final ModelD2RQ m = new ModelD2RQ(&lt;path to mapping.ttl&gt;);
final Reasoner reasoner = &lt;some reasoner&gt;;
final InfModel ontModel = ModelFactory.createInfModel(reasoner, m);

final String sparql = &lt;query&gt;

final Query q = QueryFactory.create(sparql);
final ResultSet rs = QueryExecutionFactory.create(q, ontModel).execSelect();

```

网上有一些代码示例[在这里](http://www.programcreek.com/java-api-examples/com.hp.hpl.jena.rdf.model.ModelFactory)，[在这里](http://massapi.com/class/in/InfModel.html)，以及一个带有推理器和规则的 FOAF 示例[在这里](https://github.com/agastheswar/Semantic-Web-application/blob/master/HelloSemanticWeb/src/org/semweb/assign6/HelloSemanticWeb.java)。

最后，关于这个话题的一个更近期的[博客](https://blog.talentica.com/2014/08/16/semantic-web-a-technical-introduction/)帖子，也是提醒 d2rq 语言很强大，并且提供了能够自我连接的能力——[d2rq:alias](http://d2rq.org/d2rq-language#example-alias)

~ 由 mdavey 于 2016 年 5 月 17 日发表。

发布在[数据](https://mdavey.wordpress.com/category/data/)

标签：[数据湖](https://mdavey.wordpress.com/tag/datalake/)，[本体论](https://mdavey.wordpress.com/tag/ontology/)

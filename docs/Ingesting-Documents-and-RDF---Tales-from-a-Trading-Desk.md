<!--yml

类别：未分类

日期：2024-05-18 05:31:04

-->

# 处理文档和 RDF | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2016/06/10/ingesting-documents-and-rdf/#0001-01-01`](https://mdavey.wordpress.com/2016/06/10/ingesting-documents-and-rdf/#0001-01-01)

## 处理文档和 RDF

斯特兰奇，[MarkLogic](http://www.marklogic.com/)似乎有一些关于在单一数据集中处理文档和 RDF 的最佳文档，尽管这个概念并不是 MarkLogic 独有的。正如我之前在博客中提到的，还有许多其他产品，也可以使用各种开源框架和库（如 Apache [Jena](https://jena.apache.org/index.html)等）来构建自己的系统。

BBC [新闻](https://developer.marklogic.com/learn/semantics-exercises/loading-data)示例可能是迄今为止我所找到的最好的。

> 我们最初将每篇文章作为一个单独的 XHTML 文档。然后我们使用 OpenCalais 来分析文章并找出其中的实体（现实世界中的事物）。OpenCalais 发现了像人、他们的角色、地点（城市和国家）和组织这样的人类实体。在此基础上，它将个人与他们的角色联系起来，并确定文档的主题标题（类别）。例如，对于一篇新闻文章，OpenCalais 生成了三元组，指出该文章是关于战争的，识别了文章中提到的地点，并为这些地点提供了地理定位信息。

结果可以在下载的 zip 文件中看到，该文件提供了一个包含源文件（XHTML 文章）的目录和一个包含从[OpenCalais](http://www.opencalais.com/)生成的 RDF 文件的目录。RDF 文件使用 rdf:Description 来引用文章的原始 BBC 网址。正如预期的那样， both the XHTML and the RDF files are then ingested into MarkLogic。

最后，“SPARQL 和 XQuery [一起](https://developer.marklogic.com/learn/semantics-exercises/sparql-and-xquery)”展示了如何利用这两种内容结构。

想了解任何人在 MarkLogic 方面的经验，因为文章暗示了一个很酷的产品。

~ mdavey 于 2016 年 6 月 10 日。

发布在[数据](https://mdavey.wordpress.com/category/data/)

标签：[本体论](https://mdavey.wordpress.com/tag/ontology/)

<!--yml

category: 未分类

date: 2024-05-18 05:35:28

-->

# Neo4j 节点数据存储 | 交易桌面故事

> 来源：[`mdavey.wordpress.com/2016/03/14/neo4j-node-data-storage/#0001-01-01`](https://mdavey.wordpress.com/2016/03/14/neo4j-node-data-storage/#0001-01-01)

## Neo4j 节点数据存储

[Neo4j](http://neo4j.com/)（图形数据库）是一项很棒的技术。图数据库需要适当使用，它们像区块链和其他甜品店的科技一样，并不是 silver bullets。

当考虑在图数据库中存储什么数据时，很容易利用节点和节点间的链接、关系来生成一个图，并遍历这个图。不清楚的是，或者没有很好地文档化的是，你应该在节点上存储多少数据。例如，Christophe Willemsen 在 GraphAware 上关于使用 Neo4j 建模用户关注的博客和帖子有一个清晰的图优势。不明确的是，帖子本身可能是文本上的冗长，并且至少包括图片，是否也应该作为[属性/标签](http://stackoverflow.com/questions/31028504/what-is-the-difference-between-a-label-and-a-property-in-neo4j)存储在帖子节点上？

GitHub [neo4j-contrib/neo4j-faq](https://github.com/neo4j-contrib/neo4j-faq) 提供了以下内容，可能相关：

> Neo4j 目前不适用于存储 BLOBs/CLOBs。节点、关系和属性在磁盘上不是共同定位的。这可能会在未来得到改进。

第一版（不幸的是我没有最新版本）的[《图数据库》](http://graphdatabases.com/)，由 Ian Robinson、Jim Webber 和 Emil Eifrem 编写，提供了以下内容：

> 节点存储文件存储节点记录
> 
> 与 Neo4j 的大多数存储文件一样，节点存储是一个固定大小的记录存储，每个记录的长度为 9 字节。
> 
> 相应地，关系存储在关系存储文件中。
> 
> 关系存储由固定大小的记录组成——在这种情况下，每个记录的长度为 33 字节。
> 
> 除了包含图结构的节点和关系存储之外，我们还有属性存储文件。这些文件存储用户的键值对。回顾一下，Neo4j 作为一个属性图数据库，允许将属性（名称-值对）附加到节点和关系上。因此，属性存储是从节点和关系记录中引用的。
> 
> Neo4j 支持存储优化，通过直接将一些属性内联到属性存储文件中。当属性数据可以编码以适合记录的四个属性块之一或多个时，会发生这种情况。实际上这意味着电话号码和邮政编码等数据可以直接内联到属性存储文件中，而不是推送到动态存储。

回到**Christophe Willemsen**的文章，帖子应该存储在 Neo4j 中，还是存储在外面，并有一个相关的 ID 以允许与 Neo4j 的链接？

~ mdavey 于 2016 年 3 月 14 日发表。

发布在[数据](https://mdavey.wordpress.com/category/data/)分类中

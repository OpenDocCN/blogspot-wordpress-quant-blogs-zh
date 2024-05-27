`<!--yml

分类：未分类

日期：2024-05-18 05:48:57

`-->

# 技能云 - 第三部分 | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2014/06/03/skill-cloud-part-3/#0001-01-01`](https://mdavey.wordpress.com/2014/06/03/skill-cloud-part-3/#0001-01-01)

## 技能云 - 第三部分

存储技能云的一种明显方式是通过图数据库。 [Neo4j](http://www.neo4j.org/) 或 [Titan](http://thinkaurelius.github.io/titan/) 是两个可能的选择。 出于某种原因，我选择了 Neo4j，并使用 Java 的嵌入式版本来快速入门。 将 Maven [依赖项](http://docs.neo4j.org/chunked/milestone/tutorials-java-embedded-setup.html)添加到我的 pom.xml 中是开始的最简单方式。 Neo4j 的 [HelloWorld](https://github.com/neo4j/neo4j/blob/2.1.1/community/embedded-examples/src/main/java/org/neo4j/examples/EmbeddedNeo4j.java) 示例可能是作为快速启动的骨架借用的最简单的东西。

建模一个人、他们的技能和他们的团队是这个概念验证（PoC）的一个重要部分。 技能和团队成员将被建模为节点（显然），适当的关系来捕捉与一个人技能云（节点）的链接，以及团队中谁与谁一起工作 - 团队本身显然是一个节点。

这很好地引导到了 GitHub 上的“在 Neo4j 中表示时间依赖的图”页面。[GitHub](https://github.com/SocioPatterns/neo4j-dynagraph/wiki/Representing-time-dependent-graphs-in-Neo4j)。 可能有趣的是，理想情况下，您希望有一个双时态的节点和关系的视图，因为随着时间的推移，人和团队都会发生变化。

~ mdavey 于 2014 年 6 月 3 日。

发布在 [数据](https://mdavey.wordpress.com/category/data/) 分类下

<!--yml

分类：未分类

日期：2024-05-18 05:32:12

-->

# 本体论并不可怕 | 交易桌旁的 tales

> 来源：[`mdavey.wordpress.com/2016/05/13/ontologies-are-not-scary/#0001-01-01`](https://mdavey.wordpress.com/2016/05/13/ontologies-are-not-scary/#0001-01-01)

## 本体论并不可怕

[FOAF](http://xmlns.com/foaf/spec/)对本体论的描述非常好：

> FOAF 使用受网络启发的基本概念来描述世界。在 FOAF 描述中，只有各种事物和链接，我们称之为属性。我们在 FOAF 中谈论的事物类型称为类。因此，FOAF 被定义为一个术语字典，每个术语都是类或属性之一。与 FOAF 并行的其他项目提供了其他类和属性的集合，其中许多与 FOAF 中定义的类和属性相链接。

在[D2RQ](http://d2rq.org/d2rq-language)的世界里，关键在于 mapping.ttl 文件，该文件将关系型世界（表和列）映射到本体论世界（类和属性）。

基于上述内容，再读一些相关资料，你可以定义自己的本体论，或者使用现成的开源本体论：

```

@prefix rdf: &amp;lt;http://www.w3.org/1999/02/22-rdf-syntax-ns#&amp;gt; .
@prefix rdfs: &amp;lt;http://www.w3.org/2000/01/rdf-schema#&amp;gt; .
@prefix owl: &amp;lt;http://www.w3.org/2002/07/owl#&amp;gt; .
@prefix xsd: &amp;lt;http://www.w3.org/2001/XMLSchema#&amp;gt; .

@prefix mydatalake: &amp;lt;http://www.something.com/mydatalake-schema#&amp;gt; .

mydatalake:SomeThing a owl:Class;
 rdfs:label "Something label"

iondatalake:SomeThingProperty a owl:FunctionalProperty;
 rdfs:label "SomeThingProperty label"
 rdfs:domain mydatalake:SomeThing
rdfs:range rdfs:Literal

&lt;br data-mce-bogus="1"&gt;

```

接着是 D2RQ 的 mapping.ttl，允许您对数据存储执行 SPARSQL：

```

@prefix mydatalake: &amp;lt;http://www.something.com/mydatalake-schema#&amp;gt; .
@prefix db: &amp;lt;&amp;gt; .
@prefix vocab: &amp;lt;vocab/&amp;gt; .
@prefix rdf: &amp;lt;http://www.w3.org/1999/02/22-rdf-syntax-ns#&amp;gt; .
@prefix rdfs: &amp;lt;http://www.w3.org/2000/01/rdf-schema#&amp;gt; .
@prefix xsd: &amp;lt;http://www.w3.org/2001/XMLSchema#&amp;gt; .
@prefix d2rq: &amp;lt;http://www.wiwiss.fu-berlin.de/suhl/bizer/D2RQ/0.1#&amp;gt; .
@prefix jdbc: &amp;lt;http://d2rq.org/terms/jdbc/&amp;gt; .
@prefix foaf: &amp;lt;http://xmlns.com/foaf/0.1/&amp;gt; .

mydatalake:database a d2rq:Database;
 d2rq:jdbcDriver "org.apache.phoenix.jdbc.PhoenixDriver";
 d2rq:jdbcDSN "jdbc:phoenix:localhost";
 jdbc:autoReconnect "true";
 jdbc:zeroDateTimeBehavior "convertToNull";
 .

mydatalake:STOCK_SYMBOL a d2rq:ClassMap;
 d2rq:dataStorage mydatalake:database;
 d2rq:uriPattern "STOCK_SYMBOL";
 d2rq:class mydatalake:SomeThing;
 .
mydatalake:STOCK_SYMBOL_SYMBOL a d2rq:PropertyBridge;
 d2rq:belongsToClassMap mydatalake:STOCK_SYMBOL;
 d2rq:property foaf:name;
 d2rq:column "STOCK_SYMBOL.SYMBOL";
 .

```

这进而打开了世界，通过 Apache Jena 项目使用[推理器](https://jena.apache.org/documentation/inference/)和规则引擎。

~ mdavey 于 2016 年 5 月 13 日。

发布在[数据](https://mdavey.wordpress.com/category/data/)分类下

标签：[数据湖](https://mdavey.wordpress.com/tag/datalake/)，[本体论](https://mdavey.wordpress.com/tag/ontology/)

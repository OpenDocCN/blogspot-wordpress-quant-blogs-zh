<!--yml
category: 未分类
date: 2024-05-18 05:32:12
-->

# Ontologies Are Not Scary | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/05/13/ontologies-are-not-scary/#0001-01-01](https://mdavey.wordpress.com/2016/05/13/ontologies-are-not-scary/#0001-01-01)

## Ontologies Are Not Scary

[FOAF](http://xmlns.com/foaf/spec/) offers great description of what an Ontology is:

> FOAF describes the world using simple ideas inspired by the Web. In FOAF descriptions, there are only various kinds of things and links, which we call properties. The types of the things we talk about in FOAF are called classes. FOAF is therefore defined as a dictionary of terms, each of which is either a class or a property. Other projects alongside FOAF provide other sets of classes and properties, many of which are linked with those defined in FOAF.

In the [D2RQ](http://d2rq.org/d2rq-language) world, the key is the mapping.ttl file, which maps the relational world (tables and columns) to the Ontology world (classes and properties).

Given the above, and a bit of reading, you can define your own ontology, or use readily available open source ontologies:

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

Followed by a D2RQ mapping.ttl to allow SPARSQL against your datastore:

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

Which then opens up the world to [reasoners](https://jena.apache.org/documentation/inference/) and rule engines thought the Apache Jena project.

~ by mdavey on May 13, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/)
Tags: [DataLake](https://mdavey.wordpress.com/tag/datalake/), [Ontology](https://mdavey.wordpress.com/tag/ontology/)
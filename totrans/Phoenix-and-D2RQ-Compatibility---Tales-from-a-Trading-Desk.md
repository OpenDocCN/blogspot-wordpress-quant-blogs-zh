<!--yml
category: 未分类
date: 2024-05-18 05:32:16
-->

# Phoenix and D2RQ Compatibility | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/05/12/phoenix-and-d2rq-compatibility/#0001-01-01](https://mdavey.wordpress.com/2016/05/12/phoenix-and-d2rq-compatibility/#0001-01-01)

If you happen to want to follow an [AllegroGraph](http://allegrograph.com/allegrograph/) view of Semantic data lakes, but with an Open Source stack, you may venture down the [Phoenix](https://phoenix.apache.org/) and [D2RQ](http://d2rq.org/) road.  Be aware of an issue that isn’t obvious – class path hell.

If you following the D2RQ [instructions](http://d2rq.org/getting-started), you’ll run into an issue with the Phoenix driver (the latest being phoenix-4.7.0-HBase-1.1-client.jar).  Loading the Phoenix driver to early on the classpath generates this issue:

> WARN ContextHandler :: Empty contextPath
> WARN AbstractLifeCycle :: FAILED o.e.j.w.WebAppContext@1e0b4072{/,null,null},webapp: java.lang.NoSuchMethodError: org.eclipse.jetty.server.Connector.getHost()Ljava/lang/String;
> java.lang.NoSuchMethodError: org.eclipse.jetty.server.Connector.getHost()Ljava/lang/String;
> at org.eclipse.jetty.webapp.WebInfConfiguration.getCanonicalNameForWebAppTmpDir(WebInfConfiguration.java:598)
> at org.eclipse.jetty.webapp.WebInfConfiguration.makeTempDirectory(WebInfConfiguration.java:343)
> at org.eclipse.jetty.webapp.WebInfConfiguration.resolveTempDirectory(WebInfConfiguration.java:282)

However, if you move the Phoenix driver to the end of the classpath, or close to the end, all is resolved 🙂

If you use the STOCK_SYMBOL.sql found in the Phoenix examples folder, you can then run the following SPARSQL query via the D2RQ Snorql web service:

```

SELECT ?r
WHERE {?n vocab:STOCK_SYMBOL_SYMBOL ?r }
ORDER BY DESC(?r)

```

Although basic, it at least shows that you’ve managed to get HBase data back via SPARSQL, assuming your mapping.ttl looks at minimal like the below:

```

@prefix map: <#> .
@prefix db: <> .
@prefix vocab: <vocab/> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
@prefix d2rq: <http://www.wiwiss.fu-berlin.de/suhl/bizer/D2RQ/0.1#> .
@prefix jdbc: <http://d2rq.org/terms/jdbc/> .
@prefix foaf: <http://xmlns.com/foaf/0.1/> .

map:database a d2rq:Database;
d2rq:jdbcDriver "org.apache.phoenix.jdbc.PhoenixDriver";
d2rq:jdbcDSN "jdbc:phoenix:localhost";
jdbc:autoReconnect "true";
jdbc:zeroDateTimeBehavior "convertToNull";
.

# Table group_personnel
map:STOCK_SYMBOL a d2rq:ClassMap;
d2rq:dataStorage map:database;
d2rq:uriPattern "STOCK_SYMBOL";
d2rq:class vocab:STOCK_SYMBOL;
d2rq:classDefinitionLabel "STOCK_SYMBOL";
.
map:STOCK_SYMBOL_SYMBOL a d2rq:PropertyBridge;
d2rq:belongsToClassMap map:STOCK_SYMBOL;
d2rq:property vocab:STOCK_SYMBOL_SYMBOL;
d2rq:propertyDefinitionLabel "STOCK_SYMBOL SYMBOL";
d2rq:column "STOCK_SYMBOL.SYMBOL";
.

```

~ by mdavey on May 12, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/), [HPC](https://mdavey.wordpress.com/category/hpc/)
Tags: [DataLake](https://mdavey.wordpress.com/tag/datalake/), [Ontology](https://mdavey.wordpress.com/tag/ontology/)
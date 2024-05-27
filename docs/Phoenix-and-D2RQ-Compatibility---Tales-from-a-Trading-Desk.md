`<!--yml`

分类：未分类

日期：2024-05-18 05:32:16

`-->`

# Phoenix 和 D2RQ 兼容性 | 交易桌边的传说

> 来源：[`mdavey.wordpress.com/2016/05/12/phoenix-and-d2rq-compatibility/#0001-01-01`](https://mdavey.wordpress.com/2016/05/12/phoenix-and-d2rq-compatibility/#0001-01-01)

如果你恰好想要遵循一个[AllegroGraph](http://allegrograph.com/allegrograph/)的语义数据湖视图，但又想使用开源栈，你可能会走向 Phoenix 和[D2RQ](http://d2rq.org/)的道路。要注意一个不明显的问题——类路径地狱。

如果你遵循 D2RQ [说明](http://d2rq.org/getting-started)，你将遇到一个与 Phoenix 驱动程序有关的问题（最新的是`phoenix-4.7.0-HBase-1.1-client.jar`）。在类路径的早期加载 Phoenix 驱动程序会产生这个问题：

> 警告 ContextHandler :: 空 contextPath
> 
> 警告 AbstractLifeCycle :: 失败 o.e.j.w.WebAppContext@1e0b4072{/,null,null},webapp: java.lang.NoSuchMethodError: org.eclipse.jetty.server.Connector.getHost()Ljava/lang/String;
> 
> `java.lang.NoSuchMethodError: org.eclipse.jetty.server.Connector.getHost()Ljava/lang/String;`
> 
> 在`org.eclipse.jetty.webapp.WebInfConfiguration.getCanonicalNameForWebAppTmpDir(WebInfConfiguration.java:598)`
> 
> 在`org.eclipse.jetty.webapp.WebInfConfiguration.makeTempDirectory(WebInfConfiguration.java:343)`
> 
> 在`org.eclipse.jetty.webapp.WebInfConfiguration.resolveTempDirectory(WebInfConfiguration.java:282)`

然而，如果你将 Phoenix 驱动程序移到类路径的末尾，或接近末尾，一切都会解决：）

如果你使用 Phoenix 示例文件夹中的`STOCK_SYMBOL.sql`，你然后可以通过 D2RQ Snorql 网络服务运行以下 SPARSQL 查询：

```

SELECT ?r
WHERE {?n vocab:STOCK_SYMBOL_SYMBOL ?r }
ORDER BY DESC(?r)

```

虽然基础，但至少表明你已经通过 SPARSQL 成功恢复了 HBase 数据，假设你的 mapping.ttl 看起来像下面这样：

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

~ mdavey 于 2016 年 5 月 12 日

发布在[数据](https://mdavey.wordpress.com/category/data/)，[高性能计算](https://mdavey.wordpress.com/category/hpc/)

标签：[数据湖](https://mdavey.wordpress.com/tag/datalake/)，[本体](https://mdavey.wordpress.com/tag/ontology/)

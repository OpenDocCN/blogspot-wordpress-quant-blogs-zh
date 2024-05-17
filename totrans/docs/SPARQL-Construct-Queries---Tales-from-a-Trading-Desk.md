<!--yml
category: 未分类
date: 2024-05-18 05:31:46
-->

# SPARQL Construct Queries | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/05/19/sparql-construct-queries/#0001-01-01](https://mdavey.wordpress.com/2016/05/19/sparql-construct-queries/#0001-01-01)

## SPARQL Construct Queries

Nice [example](http://docs.oracle.com/cd/E26161_02/html/RDFGraph/example8.html) of what you can do with SPARQL.  Model from a Model 🙂

```
<pre class="programlisting">Query query = QueryFactory.create(szQuery) ;
QueryExecution qexec = QueryExecutionFactory.create(query, model);

Model constructModel = qexec.execConstruct();
System.out.println("Construct result = " + constructModel.toString());
</pre>

```

~ by mdavey on May 19, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/)
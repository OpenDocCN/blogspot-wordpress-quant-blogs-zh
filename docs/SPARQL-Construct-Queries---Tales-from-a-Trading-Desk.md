<!--yml

分类：未分类

日期：2024-05-18 05:31:46

-->

# SPARQL 构造查询 | 交易桌旁的故事

> 来源：[`mdavey.wordpress.com/2016/05/19/sparql-construct-queries/#0001-01-01`](https://mdavey.wordpress.com/2016/05/19/sparql-construct-queries/#0001-01-01)

## SPARQL 构造查询

这是一个很好的[示例](http://docs.oracle.com/cd/E26161_02/html/RDFGraph/example8.html)，展示了你可以用 SPARQL 做什么。 模型来自一个模型😊

```
<pre class="programlisting">Query query = QueryFactory.create(szQuery) ;
QueryExecution qexec = QueryExecutionFactory.create(query, model);

Model constructModel = qexec.execConstruct();
System.out.println("Construct result = " + constructModel.toString());
</pre>

```

~ mdavey 于 2016 年 5 月 19 日发表。

发布于[数据](https://mdavey.wordpress.com/category/data/)

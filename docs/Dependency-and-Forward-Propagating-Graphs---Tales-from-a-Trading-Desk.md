<!--yml

类别：未分类

日期：2024 年 05 月 18 日 05:58:14

-->

# 依赖关系和正向传播图 | 交易台的故事

> 来源：[`mdavey.wordpress.com/2013/11/11/dependency-and-forward-propagating-graphs/#0001-01-01`](https://mdavey.wordpress.com/2013/11/11/dependency-and-forward-propagating-graphs/#0001-01-01)

## 依赖关系和正向传播图

尽管我之前已经博客过有关阿泰纳的内容，但重新阅读 JPM [职业生涯](http://techcareers.jpmorgan.com/cm/BlobServer/athena_jpmc.pdf?blobkey=id&blobwhere=1320615212303&blobheader=application/pdf&blobheadername1=Cache-Control&blobheadervalue1=private&blobcol=urldata&blobtable=MungoBlobs) 数据的内容仍然值得一读。

> 依赖图 - 开发人员定义特别装饰的 Python 类来表示市场、金融工具和交易。 一个运行时解析器检查这些类来构建一个内存中的
> 
> [依赖](http://bigblog.tanbin.com/2010/11/secdb-schemaless-graph-database.html)
> 
> 表示它们之间关系的图。 这提供了一种自然而强大的方法来通过移动市场利率并检查由此产生的价格的影响来探索“假设”场景。
> 
> (阿泰纳反应性) 框架的核心是一个正向传播图，其中的节点包含按照它们在图中的排名（拓扑排序顺序）调度执行的工作单元。

~ 作者 mdavey，于 2013 年 11 月 11 日发布。

发布在[语言](https://mdavey.wordpress.com/category/languages/)类别中

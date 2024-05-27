<!--yml

分类：未分类

日期：2024-05-18 05:36:53

-->

# 学会爱上日志文件 | 交易桌旁的故事

> 来源：[`mdavey.wordpress.com/2016/01/06/learn-to-love-log-files/#0001-01-01`](https://mdavey.wordpress.com/2016/01/06/learn-to-love-log-files/#0001-01-01)

## 学会爱上日志文件

绝大多数软件项目在起步时都没有考虑过日志文件应包含哪些内容。日志文件在软件开发思维过程中实际上是一个第三类公民。我见过一些公司规定日志文件中必须包含某些数据，以帮助项目从开发过渡到生产——基础设施和应用程序的支持交接。在使用[ELK](https://www.elastic.co/products)一段时间后，我意识到[ELK](http://brewhouse.io/blog/2014/11/04/big-data-with-elk-stack.html)是开发团队“自食其果”的一个简单方法。

以下是我认为有用的几点建议：

+   在使用 logstash 时快速熟悉[grok](https://www.elastic.co/guide/en/logstash/current/plugins-filters-grok.html)

+   当我开始接触 ELK 时，我不幸地摄入了没有得到 grok 适当处理的日志文件。[删除](https://www.elastic.co/guide/en/elasticsearch/reference/1.3/docs-delete-by-query.html)文档作为查询是有帮助的。

+   索引库（Index’s）很重要：）

~ mdavey 于 2016 年 1 月 6 日。

发表于[数据](https://mdavey.wordpress.com/category/data/)

标签：[ELK](https://mdavey.wordpress.com/tag/elk/)

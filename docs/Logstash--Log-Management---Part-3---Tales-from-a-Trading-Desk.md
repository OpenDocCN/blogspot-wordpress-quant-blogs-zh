<!--yml

category: 未分类

date: 2024-05-18 05:36:15

-->

# Logstash：日志管理–第三部分 | 一个交易台的故事

> 来源：[`mdavey.wordpress.com/2016/01/29/logstash-log-management-part-3/#0001-01-01`](https://mdavey.wordpress.com/2016/01/29/logstash-log-management-part-3/#0001-01-01)

## Logstash：日志管理–第三部分

正如我怀疑的那样，当你踏上 ELK 之路时，你会意识到你没有足够的磁盘空间来存储所有的日志。 幸运的是，[Curator](https://www.elastic.co/guide/en/elasticsearch/client/curator/current/examples.html)来拯救了。 其中最基本和简单的命令之一是：

> curator show indices –all-indices

还值得知道[目录](https://www.elastic.co/guide/en/elasticsearch/reference/current/setup-dir-layout.html)的布局等节点

~ 由 mdavey 于 2016 年 1 月 29 日发布。

发表在[数据](https://mdavey.wordpress.com/category/data/)中

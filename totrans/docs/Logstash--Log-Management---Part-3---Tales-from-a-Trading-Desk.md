<!--yml
category: 未分类
date: 2024-05-18 05:36:15
-->

# Logstash: Log Management – Part 3 | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/01/29/logstash-log-management-part-3/#0001-01-01](https://mdavey.wordpress.com/2016/01/29/logstash-log-management-part-3/#0001-01-01)

## Logstash: Log Management – Part 3

As I suspect is the usual course venturing down the ELK road, at some point you realise you don’t have enough disk space for all the logs you are consuming.   Luckily, [Curator](https://www.elastic.co/guide/en/elasticsearch/client/curator/current/examples.html) comes to the rescue.  One of the most basic and simple commands is:

> curator show indices –all-indices

Its also worth knowing the [directory](https://www.elastic.co/guide/en/elasticsearch/reference/current/setup-dir-layout.html) layout of the nodes etc

~ by mdavey on January 29, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/)
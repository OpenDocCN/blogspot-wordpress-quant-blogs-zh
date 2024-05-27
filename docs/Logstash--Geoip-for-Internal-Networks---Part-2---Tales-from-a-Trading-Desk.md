<!--yml

category: 未分类

date: 2024-05-18 05:36:24

-->

# Logstash: 内部网络的 Geoip – 第二部分 | 交易桌上的故事

> 来源：[`mdavey.wordpress.com/2016/01/20/logstash-geoip-for-internal-networks-part-2/#0001-01-01`](https://mdavey.wordpress.com/2016/01/20/logstash-geoip-for-internal-networks-part-2/#0001-01-01)

## Logstash: 内部网络的 Geoip – 第二部分

继续讲解 logstash。如果你的工作涉及到 TopBeat，那么请考虑这些仪表板，它们[在这里](https://www.elastic.co/guide/en/beats/libbeat/1.0.1/getting-started.html#load-kibana-dashboards)可用。使用 FileBeats 和 TopBeats 来喂养 logstash，实际上意味着 logstash 通过端口 5044 接收两个数据流。在你的 logstash 配置中，你可能希望将数据插入到不同的 ElasticSearch 索引中。做到这一点的一种方法是检查来自 Beats 的数据的输入类型：

filter {

if [type] == “system” or [type] == “filesystem” or [type] == “process” {

mutate {

add_field => { “_IndexName” => “%{type}” }

}

And then in the output section, change the index name as appropriate:

elasticsearch {

index => “%{_IndexName}-%{+YYYY.MM.dd}”

~ by mdavey on January 20, 2016.

Posted in [数据](https://mdavey.wordpress.com/category/data/)

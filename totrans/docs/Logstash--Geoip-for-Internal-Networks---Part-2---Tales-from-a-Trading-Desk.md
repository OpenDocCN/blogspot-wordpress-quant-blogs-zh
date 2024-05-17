<!--yml
category: 未分类
date: 2024-05-18 05:36:24
-->

# Logstash: Geoip for Internal Networks – Part 2 | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/01/20/logstash-geoip-for-internal-networks-part-2/#0001-01-01](https://mdavey.wordpress.com/2016/01/20/logstash-geoip-for-internal-networks-part-2/#0001-01-01)

## Logstash: Geoip for Internal Networks – Part 2

Continuing with logstash.  If your doing anything with TopBeat, then consider the dashboards, available [here](https://www.elastic.co/guide/en/beats/libbeat/1.0.1/getting-started.html#load-kibana-dashboards).  Using FileBeats and TopBeats to feed logstash, will effectively mean logstash receives both streams via port 5044\.  In your logstash config, your may want to insert the data into different ElasticSearch index’s.  One way tot do this is to check the input type of data from Beats:

filter {

 if [type] == “system” or [type] == “filesystem” or [type] == “process” {

 mutate {

 add_field => { “_IndexName” => “%{type}” }

 }

And then in the output section, change the index name as appropriate:

 elasticsearch {

 index => “%{_IndexName}-%{+YYYY.MM.dd}”

~ by mdavey on January 20, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/)
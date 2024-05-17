<!--yml
category: 未分类
date: 2024-05-18 05:36:49
-->

# Logstash: Geoip for Internal Networks | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/01/07/logstash-geoip-for-internal-networks/#0001-01-01](https://mdavey.wordpress.com/2016/01/07/logstash-geoip-for-internal-networks/#0001-01-01)

## Logstash: Geoip for Internal Networks

Continuing down the ELK road, I ran into the issue of internal log files having internal network addresses, which when using the Kibana map facility, isn’t very helpful.  However, thanks to a number of articles and posting on the web, this is completely solvable. Vlad Ionescu [posting](https://blog.vladionescu.com/geo-location-for-internal-networks/) is particularly useful, leveraging the GeoLite City data.  Another [solution](https://discuss.elastic.co/t/creating-geoip-data-for-internal-networks/729), in many ways a quick fix, is offered by Jim Cheetham.  Finally, this posting offer a view on the geoip logstash properties to set to specify the GeoLite City database [location](https://www.digitalocean.com/community/tutorials/how-to-map-user-location-with-geoip-and-elk-elasticsearch-logstash-and-kibana).

~ by mdavey on January 7, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/)
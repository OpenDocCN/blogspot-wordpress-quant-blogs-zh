以下为 yml 格式内容：

分类：未分类

日期：2024-05-18 05:36:49

→

# Logstash: Geoip for Internal Networks | Tales from a Trading Desk

> 来源：[`mdavey.wordpress.com/2016/01/07/logstash-geoip-for-internal-networks/#0001-01-01`](https://mdavey.wordpress.com/2016/01/07/logstash-geoip-for-internal-networks/#0001-01-01)

## Logstash: Geoip for Internal Networks

在继续深入 ELK 道路的过程中，我遇到了一个问题：内部日志文件包含内部网络地址，这在使用 Kibana 的地图功能时并不太有用。然而，多亏了网上众多文章和帖子，这个问题完全可以解决。Vlad Ionescu 的[帖子](https://blog.vladionescu.com/geo-location-for-internal-networks/)特别有用，利用了 GeoLite City 数据。另一个[解决方案](https://discuss.elastic.co/t/creating-geoip-data-for-internal-networks/729)，在很多方面是一个快速修复，由 Jim Cheetham 提供。最后，这个帖子提供了关于如何设置 geoip logstash 属性的观点，以指定 GeoLite City 数据库[位置](https://www.digitalocean.com/community/tutorials/how-to-map-user-location-with-geoip-and-elk-elasticsearch-logstash-and-kibana)。

作者：mdavey 于 2016 年 1 月 7 日。

发表于[数据](https://mdavey.wordpress.com/category/data/)分类下

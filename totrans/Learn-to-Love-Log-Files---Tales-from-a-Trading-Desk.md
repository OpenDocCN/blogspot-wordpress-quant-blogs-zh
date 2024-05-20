<!--yml
category: 未分类
date: 2024-05-18 05:36:53
-->

# Learn to Love Log Files | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/01/06/learn-to-love-log-files/#0001-01-01](https://mdavey.wordpress.com/2016/01/06/learn-to-love-log-files/#0001-01-01)

## Learn to Love Log Files

A vast majority of software projects start out with no though as to what should go into log files.  Log files are effectively a 3rd class citizen in the software development thought process.  I’ve seen a few companies mandate certain data in log files for projects to ease the transition from development to production – handover to support (both infrastructure and application).  Having spent some time using [ELK](https://www.elastic.co/products), ingesting log files from applications that really aren’t structured very well, I now believe that [ELK](http://brewhouse.io/blog/2014/11/04/big-data-with-elk-stack.html) is an easy way for development teams to eat their own dog food.

What follows are a few points that I found useful:

*   Get familiar with [grok](https://www.elastic.co/guide/en/logstash/current/plugins-filters-grok.html) fast when using logstash
*   When I started out with ELK, I unfortunately ingested log files that didn’t get grok’s appropriate.  [Deleting](https://www.elastic.co/guide/en/elasticsearch/reference/1.3/docs-delete-by-query.html) document is thus helpful as a query.
*   [Index’s](https://www.elastic.co/guide/en/kibana/current/tutorial-define-index.html) are important 🙂

~ by mdavey on January 6, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/)
Tags: [ELK](https://mdavey.wordpress.com/tag/elk/)
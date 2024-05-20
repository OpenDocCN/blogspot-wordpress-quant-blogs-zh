<!--yml
category: 未分类
date: 2024-05-18 05:32:29
-->

# SPARQL Data Platform | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/05/10/sparql-data-platform/#0001-01-01](https://mdavey.wordpress.com/2016/05/10/sparql-data-platform/#0001-01-01)

## SPARQL Data Platform

Given the various postings on SPARQL recently, I thought it worth noting down the various data platform options I’ve considered:

1.  For pure PoC’ing, MySQL using the file import facility in MySQLWorkbench, running [D2RQ](http://d2rq.org/getting-started) to provide SPARQL access.  Simple, and easy to setup.
2.  For more of a Hadoop platform, [HBase](https://hbase.apache.org/) with Apache [Phoenix](https://phoenix.apache.org/) offering a JDBC driver, again allowing D2RQ to be used as the SPARQL access layer.
3.  Apache [Marmotta](http://marmotta.apache.org/), in many ways an improvement on Option 1 above, since it sits on top of standard [database](http://marmotta.apache.org/installation.html) technology.

Option 1 is probably the quickest to move forwards with, once you’ve become annoyed with accessing corporate data that is spread across n systems, and your still in Machine Learning Discovery land 🙂  If you’ve used Apache Marmotta, or have time to set it up and learning the platform, Option 3 maybe a better bet.

Option 2 is probably the production version, or at least a stab in the right direction, as it offers improvements on scaling, coupled with Hadoopness 🙂

Where’s all this going?  “[SPARQL](http://www.r-bloggers.com/sparql-with-r-in-less-than-5-minutes/) with R in less than 5 minutes” provide a quick and interesting read on the power of SPARQL.  If your building a data lake without a foundation (ontology), you maybe missing a trick.

Interested in anyone else’s options

~ by mdavey on May 10, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/)
Tags: [DataLake](https://mdavey.wordpress.com/tag/datalake/), [Ontology](https://mdavey.wordpress.com/tag/ontology/), [RDF](https://mdavey.wordpress.com/tag/rdf/)
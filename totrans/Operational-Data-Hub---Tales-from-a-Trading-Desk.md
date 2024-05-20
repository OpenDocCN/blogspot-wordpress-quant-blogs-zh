<!--yml
category: 未分类
date: 2024-05-18 05:31:12
-->

# Operational Data Hub | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/06/10/operational-data-hub/#0001-01-01](https://mdavey.wordpress.com/2016/06/10/operational-data-hub/#0001-01-01)

## Operational Data Hub

Although bias to [Marklogic](http://www.marklogic.com/blog/eliminate-data-silos-multi-model-database/), “Decimating Data Silos With Multi-Model Databases” provides an interesting.  Few interesting take aways:

> 60 percent of the cost of a new data warehousing project is allocated to ETL and corporations spend $36 billion annually on creating relational data silos.

Of no surprise is the “semantic metadata” concept, and also the callout to ELT over ETL.

Three approaches to avoiding ETL hell:

1.  A [semantics](http://www.marklogic.com/what-is-marklogic/features/semantics/) triple store/graph-only architecture
2.  A document store-only architecture
3.  A multi-model approach that combines a document store and triple store

On Option 2, “Defensive programming for unexpected data structures” is so true based on what I’ve seen

Agree that Option 3 is the preference, and best of both worlds (document storage and ontology).  Not being a Marklogic expert is about appear in many ways that this is similar to combining [MongoDB](https://www.mongodb.com/) or similar with [D2RQ](http://d2rq.org)?

~ by mdavey on June 10, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/)
Tags: [Ontology](https://mdavey.wordpress.com/tag/ontology/)
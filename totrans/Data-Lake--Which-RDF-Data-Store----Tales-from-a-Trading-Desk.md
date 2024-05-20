<!--yml
category: 未分类
date: 2024-05-18 05:32:46
-->

# Data Lake: Which RDF Data Store? | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/05/03/which-rdf-data-store/#0001-01-01](https://mdavey.wordpress.com/2016/05/03/which-rdf-data-store/#0001-01-01)

## Data Lake: Which RDF Data Store?

A number of triple stores are listed [here](https://www.w3.org/2001/sw/wiki/Java).  GraphDB looks [interesting](http://graphdb.ontotext.com/graphdb/), but I suspect the enterprise edition tips the scale towards an Open Source solution.  In the world of big data, I suspect you really want SPARSQL over [Hadoop](https://jena.apache.org/documentation/hadoop/)?

> store data in a key value store in Hadoop [Hbase], but then index it with our [graph](http://www.datanami.com/2015/05/26/hadoop-triple-stores-and-the-semantic-data-lake/) database so that we can do these SPARQL queries

This is echo’d by “Avoiding Three Common [Pitfalls](http://data-informed.com/avoiding-three-common-pitfalls-data-lakes/) of Data Lakes”:

> Smart data technologies substantially reduce the complexity of data lake implementations while accelerating the time-to-value they produce. The graph-based model and detailed descriptions of data elements they enable substantially enhance integration efforts, enabling business users to link data according to relevant attributes that provide pivotal context across data sources and business models. Resource Description Framework (RDF) graphs are designed to incorporate new data and sources without having to re-configure existing representations. The result is considerably decreased time to a more profound form of analytics, in which users can not only ask more questions more expediently than before, but also determine relationships and data context to issue ad-hoc queries for specific needs.

Although older, still of interest “Storing (and querying) RDF in [NoSQL](http://www.snee.com/bobdc.blog/2013/12/storing-and-querying-rdf-in-no.html) database managers”

> The paper then describes the storage and querying of RDF using HBase with Jena for querying, HBase with Hive as the query engine (with Jena’s ARQ to parse the queries before converting them to HiveQL), CumulusRDF (Cassandra with Sesame), and Couchbase

Which leads to the following possible options:

*   RDF data store used to index your data lake
*   [D2R](http://d2rq.org/) on top of your data lake

Anyone got a view?

~ by mdavey on May 3, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/)
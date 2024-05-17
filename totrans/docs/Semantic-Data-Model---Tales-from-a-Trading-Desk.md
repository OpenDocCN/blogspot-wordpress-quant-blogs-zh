<!--yml
category: 未分类
date: 2024-05-18 05:32:33
-->

# Semantic Data Model | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/05/09/semantic-data-model/#0001-01-01](https://mdavey.wordpress.com/2016/05/09/semantic-data-model/#0001-01-01)

## Semantic Data Model

“When Hadoop Simply Isn’t Enough: How to Purpose-Build Architecture for Industrial Data” offer an interesting [read](http://insidebigdata.com/2015/12/07/when-hadoop-simply-isnt-enough-how-to-purpose-build-architecture-for-industrial-data/), but not a mention of RDF’s.  ElasticSearch and Hadoop are mentioned as part of the solution, but I’m not clear on how linkage of data is achieved.  Am I missing something?

“The Data Lake Concept Is [Maturing](http://cacm.acm.org/news/200095-the-data-lake-concept-is-maturing/fulltext)” however provide a more interesting read, with Apache Hadoop Distributed File System being call out for storage, coupled with:

> when selecting a NoSQL database with which to work with their Hadoop clusters. MongoDB, he said, is typically used for department-level cache applications, Apache Cassandra for highly distributed interactive applications, and Apache [Hbase](https://hbase.apache.org/) for analytic applications which Bodkin said “can tolerate a bit more latency, having a smaller number of places where machine-learned models sit right next to your compute cluster in Hadoop.”

From a [Graph](http://www.snee.com/bobdc.blog/2014/01/storing-and-querying-rdf-in-ne.html) database perspective, an interesting article on [Neo4j](http://michaelbloggs.blogspot.co.uk/2013/05/importing-ttl-turtle-ontologies-in-neo4j.html) and RDF’s, “Importing ttl (Turtle) ontologies in Neo4j”

[Sempala](http://www.slideshare.net/alexschaetzle/sempala-iswc-2014) research is interesting, but I don’t see the code anywhere.

Finally, to [Spark](http://www.snee.com/bobdc.blog/2015/03/spark-and-sparql-rdf-graphs-an.html) and SPARQL, “RDF Graphs and [GraphX](http://www.snee.com/bobdc.blog/2015/03/spark-and-sparql-rdf-graphs-an.html)“.

Which still leads to the question of what is the latest data lake software stack?  Is the road [HBase](http://hbase.apache.org/book.html#arch.overview) to hold the [data](http://www.tutorialspoint.com/hbase/hbase_create_data.htm) and/or the RDF’s? [Jena-HBase](http://ceur-ws.org/Vol-914/paper_14.pdf)  Or is HBase paired with a separate  graph [database](http://www.datanami.com/2015/05/26/hadoop-triple-stores-and-the-semantic-data-lake/) offering SPARQL queries?

~ by mdavey on May 9, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/)
Tags: [DataLake](https://mdavey.wordpress.com/tag/datalake/), [Ontology](https://mdavey.wordpress.com/tag/ontology/)
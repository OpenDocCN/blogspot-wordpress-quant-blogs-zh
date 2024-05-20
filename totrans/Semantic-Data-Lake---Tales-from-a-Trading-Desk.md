<!--yml
category: 未分类
date: 2024-05-18 05:33:11
-->

# Semantic Data Lake | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/04/28/semantic-data-lake/#0001-01-01](https://mdavey.wordpress.com/2016/04/28/semantic-data-lake/#0001-01-01)

## Semantic Data Lake

Continuing on the data lake road, Kafka [Connect](http://www.confluent.io/blog/how-to-build-a-scalable-etl-pipeline-with-kafka-connect) look very interesting from a way to feed a data lake.  This leads to “Prototype of [Data](http://xlime.eu/images/Deliverables/xLiMe_D1.2_Prototype_of_Data_Processing_Infrastructure.pdf) Processing Infrastructure”, and usage of RDF and CumulusRDF.  RDF if interesting since its gained uptake due to [SPARQL](https://en.wikipedia.org/wiki/SPARQL) – semantic web.

Further searching of the web yields a very interesting article in the data analytics space, “Advanced Real-Time Healthcare [Analytics](https://www.linkedin.com/pulse/advanced-real-time-healthcare-analytics-apache-spark-joel-amoussou) with Apache Spark”.  Thankfully the article provide an appropriate architecture diagram, which is nicely using Apache Kafka 🙂  More interesting is that its using Ontologies:

> The architecture is hybrid and also includes a production rule engine and an ontology reasoner. This is done in order to leverage existing clinical domain knowledge available from evidence-based clinical practice guidelines (CPGs) and biomedical ontologies like SNOMED. This approach complements machine learning algorithms’ probabilistic approach to clinical decision making under uncertainty. The production rule system can translate CPGs into executable rules which are fully integrated with clinical processes (workflows) and events. Drools supports both forward and backward chaining as well as the modeling of business processes (clinical workflows) with the business process modeling notation (BPMN). There are patterns for integrating rules and processes.

Interestingly, there is a W3C Machine Learning Schema Community [Group](https://www.w3.org/community/ml-schema/) – RDF etc. There’s also a list of [projects](http://aksw.org/Groups/MOLE.html) on the Machine Learning and Ontology Engineering site.

Moving on, we find “Hadoop, Triple [Stores](http://www.dataversity.net/data-lakes-get-smart-with-semantic-graph-models/), and the [Semantic](http://www.datanami.com/2015/05/26/hadoop-triple-stores-and-the-semantic-data-lake/) Data [Lake](http://allegrograph.com/semantic-data-lake/)“:

> “What we’re investing most of our time in now is the semantic data lake, where we store data in a key value store in Hadoop [Hbase], but then index it with our graph database so that we can do these SPARQL queries,”

~ by mdavey on April 28, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/)
Tags: [DataLake](https://mdavey.wordpress.com/tag/datalake/), [Ontology](https://mdavey.wordpress.com/tag/ontology/)
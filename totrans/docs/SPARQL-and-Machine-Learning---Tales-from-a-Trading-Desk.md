<!--yml
category: 未分类
date: 2024-05-18 05:32:58
-->

# SPARQL and Machine Learning | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/04/29/sparql-and-machine-learning/#0001-01-01](https://mdavey.wordpress.com/2016/04/29/sparql-and-machine-learning/#0001-01-01)

## SPARQL and Machine Learning

As discussed in previous postings, with the industry trend appearing to be off down the Semantic Data Lake road, its probably worth understanding the Return on Investment (ROI) for Semantic Machine Learning :

*   Today, following the [CRISP-DM](https://en.wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining) process, or at least something similar, a good degree of time is spent understanding the data, and linking different data sets together to create the appropriate data frames (H2OFrame etc) before you can start train models and tuning the model parameter.  A Semantic Data Lake should at least reduce the identification of data linkages time
*   Consuming raw data into a data lake is fine, as there is zero data loss – ELT rather than ETL.  However, with changing resources on your Data Science team, there is a degree of “learning” time about the data.  RDF’s and ontologies should reduce this.
*   [Ontology Matching](http://homes.cs.washington.edu/~pedrod/papers/hois.pdf) is something that might be quite interesting from the [EL](http://wortschatz.uni-leipzig.de/~fwitschel/papers/ekaw10.pdf) side of a data lake – reduced time in leverage new data sources in the lake.
*   With RDF underpinning your data lake, data scientist now have a degree of linkage resolve.  This is briefly discussed in “[SPARQL with R](http://www.r-bloggers.com/sparql-with-r-in-less-than-5-minutes/) in less than 5 minutes”:

> In English, our query says, “Give me the values for the attributes “fires”, “acres” and “year” wherever they are defined

I think the killer statement in this article is:

> As more data becomes available in RDF format, automated solutions for mining and analyzing the Semantic Web will become more and more useful.

Which leads us to the need for a data lake, as discussed elsewhere on the web, to be underpinned by [RDF](https://en.wikipedia.org/wiki/SPARQL).  As an example, if your lake is consuming social network data (e.g Facebook), then your probably want to look at Friend of a Friend ([FOAF](http://www.foaf-project.org/)), since this will allow you to [query](https://www.w3.org/TR/2012/WD-sparql11-overview-20120501/#sparql11-query) the data lake (of many data sources) leveraging the FOAF ontology:

```
PREFIX foaf: &lt;http://xmlns.com/foaf/0.1/&gt;
SELECT ?name (COUNT(?friend) AS ?count)
WHERE {
    ?person foaf:name ?name .
    ?person foaf:knows ?friend .
} GROUP BY ?person ?name

```

Anyone using a [Triple store](http://jena.apache.org/) for their data lake?  If so, how are you using it with the normal Hadoop/HDFS data lake world technologies?

~ by mdavey on April 29, 2016.

Posted in [Data](https://mdavey.wordpress.com/category/data/)
Tags: [MachineLearning](https://mdavey.wordpress.com/tag/machinelearning/), [Ontology](https://mdavey.wordpress.com/tag/ontology/), [RDF](https://mdavey.wordpress.com/tag/rdf/)